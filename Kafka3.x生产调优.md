---

## 基础概念

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650686295832-4732a39b-54d2-4b1c-88b5-228ea6631458.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=978&id=uf906e738&margin=%5Bobject%20Object%5D&name=image.png&originHeight=978&originWidth=1927&originalType=binary&ratio=1&rotation=0&showTitle=false&size=907445&status=done&style=none&taskId=ua5493c81-ed2c-4a4a-a5a4-49714866e15&title=&width=1927)
  
功能：缓存/消峰、解耦、异步通信 

- 缓存/消峰：秒杀场景，可以把每秒100w的请求放入消息队列，让后面10w的业务处理
- 解耦：mysql等的数据需要发到各种平台进行处理，一个一个写耦合性高，有了消息队列会解耦
- 异步通信：有些无关紧要的事不需要立即处理，可以先对用户响应了之后再去处理这个事

两种模式

- 点对点
- 发布订阅

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650686886218-ad035e8f-17c9-40e9-b603-ab295a5d0830.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=937&id=ub71f91ce&margin=%5Bobject%20Object%5D&name=image.png&originHeight=937&originWidth=1819&originalType=binary&ratio=1&rotation=0&showTitle=false&size=573935&status=done&style=none&taskId=u505baec8-6eba-47f2-bcc8-f8055d47a1e&title=&width=1819)

 kafka架构
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650687709524-a4d60130-e9b6-468f-a548-21504186833e.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=949&id=u5f962761&margin=%5Bobject%20Object%5D&name=image.png&originHeight=949&originWidth=1876&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1244152&status=done&style=none&taskId=u677670a1-af9d-423b-b70f-4663f3e65f0&title=&width=1876)



## Kafka快速入门

---


### topic
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650689373828-1ad0fd38-de0e-434c-b8b3-15d6258e78ee.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=654&id=uda9bd194&margin=%5Bobject%20Object%5D&name=image.png&originHeight=654&originWidth=1174&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172255&status=done&style=none&taskId=u311698da-ce8e-4be9-a9d7-ff0177d6c17&title=&width=1174)

查看集群所有topic
```java
bin/kafa-topic.sh --bootstrap-server hadoop102:9092 --list
```

创建一个topic
```java
bin/kafa-topic.sh --bootstrap-server hadoop102:9092 --topic first --create --partition 1 --replication-factor 3
```

查看topic详细信息
```java
bin/kafa-topic.sh --bootstrap-server hadoop102:9092 --topic first --describe
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650689759104-fe8f2d77-7222-4b11-bb17-73e3ff4166a8.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=96&id=u1253a666&margin=%5Bobject%20Object%5D&name=image.png&originHeight=96&originWidth=1886&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94654&status=done&style=none&taskId=u21fef96b-d102-4eb2-9653-f00b48918db&title=&width=1886)
此时有3哥副本，leader是2节点

修改topic
```java
bin/kafa-topic.sh --bootstrap-server hadoop102:9092 --topic first --alter --partirion 3
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650689855054-5b330498-b1ca-480c-bbe6-708f3cfbc30b.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=132&id=u800ace26&margin=%5Bobject%20Object%5D&name=image.png&originHeight=132&originWidth=1255&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87681&status=done&style=none&taskId=ue9e77daf-9918-4a44-a57e-ce4f44d71a3&title=&width=1255)


### producer

---


产生数据
```java
bin/kafka-console-producer.sh --bootstrap-server hadoop102:9002 --topic first
> hello  
```





### consumer

---


增量消费数据
```java
bin/kafka-consumer.sh --bootstrap-server hadoop102:9002 --topic first
```

从头开始消费数据
```bash
bin/kafka-consumer.sh --bootstrap-server hadoop102:9002 --topic first --from-beginning
```




## Kafka生产者原理

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650690598579-30cf7b8c-358c-4564-9661-05d787f3b861.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=921&id=u04b567f0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=921&originWidth=1887&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1123970&status=done&style=none&taskId=u4705a56c-ba7b-4045-a44f-480c25b453a&title=&width=1887)



### idea项目(异步发送)

- 创建项目
- 导入依赖

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650690719645-ea512fc0-4b05-4e2a-8aaf-65e1d7a0ca19.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=253&id=uf849c636&margin=%5Bobject%20Object%5D&name=image.png&originHeight=253&originWidth=709&originalType=binary&ratio=1&rotation=0&showTitle=false&size=125576&status=done&style=none&taskId=u34020498-f69c-4378-b9e1-2a948f76c0e&title=&width=709)

- 创建类

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650690996984-0769b7bc-f830-4c31-890c-bb629bc6b7a2.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=776&id=uc4a34f53&margin=%5Bobject%20Object%5D&name=image.png&originHeight=776&originWidth=1384&originalType=binary&ratio=1&rotation=0&showTitle=false&size=604691&status=done&style=none&taskId=u431d6049-6903-4541-944a-98f3470c307&title=&width=1384)
带回调信息的
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650691123542-f8c4ff3e-42ff-4bf6-a886-fbb15dfc5f78.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=399&id=u1660888b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=399&originWidth=1230&originalType=binary&ratio=1&rotation=0&showTitle=false&size=190787&status=done&style=none&taskId=u1f1b04ae-550c-4241-9cdc-ae1eed3797f&title=&width=1230)


### idea项目（同步）

- 添加一个get并且抛出异常就行（必须把前一批数据发送完成才能进行下一批的发送）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650691366040-b02532e3-c23b-45a9-9b78-cf1f37228b9c.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=208&id=ue7dca5fc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=208&originWidth=1168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=103827&status=done&style=none&taskId=u9540300c-f6f6-47ef-823e-4d14341a580&title=&width=1168)



## 分区

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650691762539-ffb89818-4d81-47c9-bec5-a19fd6d33e23.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=995&id=u3cf2e88d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=995&originWidth=1913&originalType=binary&ratio=1&rotation=0&showTitle=false&size=985085&status=done&style=none&taskId=u46755558-0f03-4e46-8cd9-e19c14bac6d&title=&width=1913)
### 指定分区
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650691835388-bf17112a-bf13-437b-bcaa-1d551b17fbeb.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=632&id=u067031b0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=632&originWidth=1819&originalType=binary&ratio=1&rotation=0&showTitle=false&size=483700&status=done&style=none&taskId=ue6486457-a38a-46cf-84d9-cc78d3c4b5e&title=&width=1819)
### 指定key
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650691893169-d45440e7-8f65-4a90-aec2-6be52bca28cd.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=343&id=u10cc3040&margin=%5Bobject%20Object%5D&name=image.png&originHeight=343&originWidth=1271&originalType=binary&ratio=1&rotation=0&showTitle=false&size=181830&status=done&style=none&taskId=ud9ff1b5d-ebdf-4c2b-9363-208b0bbdade&title=&width=1271)
### 粘性分区
### 自定义分区器（包含atguigu发到0分区，不包含发到1分区）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650692051798-11f40e76-2aac-4bdf-a1c7-4b124f3daa88.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=593&id=uc67f17f5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=593&originWidth=1309&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263232&status=done&style=none&taskId=ue323237c-2f0f-4e55-a51e-910b78a63e9&title=&width=1309)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650692108944-c1dd870d-e238-4da7-bbbf-872d1f09ad58.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=441&id=u327e9329&margin=%5Bobject%20Object%5D&name=image.png&originHeight=441&originWidth=1177&originalType=binary&ratio=1&rotation=0&showTitle=false&size=366639&status=done&style=none&taskId=u57b897a0-caf5-4f55-9e8f-2c64c4bd751&title=&width=1177)
### 优化（4个参数)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650692335085-85fc565c-7772-4ffa-a379-c2c78167640b.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=838&id=u7558215a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=838&originWidth=1329&originalType=binary&ratio=1&rotation=0&showTitle=false&size=611044&status=done&style=none&taskId=u4e9d6b6f-ed4a-4e7a-91bc-cc8cccddf8b&title=&width=1329)
### 数据可靠性
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650693100297-12a2ce44-97e5-47da-906e-9f10fb4bcc36.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=957&id=u86978c2d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=957&originWidth=1909&originalType=binary&ratio=1&rotation=0&showTitle=false&size=850539&status=done&style=none&taskId=u6db06d15-bb68-42b2-a415-328a24ddbef&title=&width=1909)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650693205854-8a84b1cf-3dea-4ee3-a4b5-18ebb4a11f47.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=918&id=u77a9e22f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=918&originWidth=1918&originalType=binary&ratio=1&rotation=0&showTitle=false&size=848312&status=done&style=none&taskId=u9d2b499c-2483-4fbd-aee5-8da779a1b62&title=&width=1918)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650693260268-4fea11e9-c91d-4175-89ca-33c0746abc88.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=976&id=u142e444c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=976&originWidth=1917&originalType=binary&ratio=1&rotation=0&showTitle=false&size=824489&status=done&style=none&taskId=u347af6d4-17fa-47cd-94df-7de56957524&title=&width=1917)

- java实践

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650693321512-4f47cadc-44e8-425d-af7b-1584273b0c7b.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=531&id=u1fe70b8f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=531&originWidth=1251&originalType=binary&ratio=1&rotation=0&showTitle=false&size=300535&status=done&style=none&taskId=u70cdd155-bd11-45fe-af84-9ec59e18fd2&title=&width=1251)


### 数据传递语义
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650693583486-4e58454c-19d5-42e7-810e-ea387dc31414.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=772&id=u22d368bf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=772&originWidth=1851&originalType=binary&ratio=1&rotation=0&showTitle=false&size=393181&status=done&style=none&taskId=ub893e644-0979-4fc7-9b75-227593c0317&title=&width=1851)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650693929499-184cbf5d-b43a-4cc9-a8f3-4dd5bf1292f8.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=957&id=u6da81ae8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=957&originWidth=1930&originalType=binary&ratio=1&rotation=0&showTitle=false&size=859594&status=done&style=none&taskId=uea4d7b54-f50f-4b31-b938-ad7547b1dbb&title=&width=1930)

- 事务

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650694250577-76b29f6e-cec4-4eee-aea7-52fcba0f317d.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=124&id=u884b77d5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=124&originWidth=897&originalType=binary&ratio=1&rotation=0&showTitle=false&size=88533&status=done&style=none&taskId=ue3362913-81d1-4a2c-9b84-8c6379eb4a9&title=&width=897)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650694224064-68e4282a-6136-4687-958c-02baf34ebb5d.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=598&id=ua2065bf0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=598&originWidth=1001&originalType=binary&ratio=1&rotation=0&showTitle=false&size=242214&status=done&style=none&taskId=u8d6058f2-6174-49ea-9c9d-0899240629a&title=&width=1001)


### 数据乱序问题
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650694525886-905ad963-d201-4866-87fa-4b3d781ef8b8.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=965&id=u3491d4b8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=965&originWidth=1942&originalType=binary&ratio=1&rotation=0&showTitle=false&size=751184&status=done&style=none&taskId=ub4f2485a-15fd-40fb-ba15-dacc7cb0149&title=&width=1942)



## kafka服务器

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650694956581-af44cecb-98bb-4ef1-bc61-2f30fc3a10cd.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=981&id=u637503a1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=981&originWidth=1926&originalType=binary&ratio=1&rotation=0&showTitle=false&size=861921&status=done&style=none&taskId=u0b569559-bb5c-4e2b-938d-7f26a18e73b&title=&width=1926)

### 服役服务器和退役服务器


### Kafka副本
所有副本统称为AR， AR = ISR + OSR
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650695860825-af90348a-64df-45b9-a9f1-1edb97f87e2d.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=160&id=u1e5fc3d5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=160&originWidth=1754&originalType=binary&ratio=1&rotation=0&showTitle=false&size=214285&status=done&style=none&taskId=u6cae1ca9-2d3e-4b6a-979c-3c8b010dac6&title=&width=1754)
把3干掉，AR（replicas）中210，leader会变成2
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650695948408-be754bf9-6f58-44d4-86fd-d6817ab3baf9.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=148&id=u862b853e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=148&originWidth=1224&originalType=binary&ratio=1&rotation=0&showTitle=false&size=147949&status=done&style=none&taskId=u1b577951-a338-4049-b24f-1133e295652&title=&width=1224)

### 分区存储调整
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650696619878-3e5bac7f-64e5-4226-aa41-b1299f194acf.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=781&id=u765046f3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=781&originWidth=1098&originalType=binary&ratio=1&rotation=0&showTitle=false&size=400377&status=done&style=none&taskId=u87e41912-9c03-47e9-a875-29ae234b2cf&title=&width=1098)

- 调整过后，都存储在前2台服务器上

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650696652432-ee01836a-8a34-44b7-8065-635026e6a89a.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=393&id=uee555c59&margin=%5Bobject%20Object%5D&name=image.png&originHeight=393&originWidth=1194&originalType=binary&ratio=1&rotation=0&showTitle=false&size=252219&status=done&style=none&taskId=u1c8690e8-867c-49e7-aabf-fb8b5fed0e8&title=&width=1194)


### Leader Partition自动平衡


### 增加副本因子
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650696824552-195ecc41-e1af-469c-8a09-ab69fa9c6c4b.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=624&id=u5bf0a100&margin=%5Bobject%20Object%5D&name=image.png&originHeight=624&originWidth=1131&originalType=binary&ratio=1&rotation=0&showTitle=false&size=306133&status=done&style=none&taskId=u655c67de-b889-48dd-bd2e-b140008d2cc&title=&width=1131)


### 高效读写数据
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697215542-f10d2bfc-c4d3-43e4-accf-56dd31a209b0.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=820&id=u9a234d4a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=820&originWidth=1145&originalType=binary&ratio=1&rotation=0&showTitle=false&size=509487&status=done&style=none&taskId=u788e4f8a-916b-40f7-9a95-50561eb277d&title=&width=1145)
零拷贝技术



## Kafka消费者

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697348770-691adc67-c344-4e0d-8736-7d48e8d4bc1a.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=909&id=u00ebf2ca&margin=%5Bobject%20Object%5D&name=image.png&originHeight=909&originWidth=1901&originalType=binary&ratio=1&rotation=0&showTitle=false&size=788919&status=done&style=none&taskId=u9e60f51a-7c98-4162-92d2-6674a88705c&title=&width=1901)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697453695-7b70d86b-0605-427b-bc3f-7dec50d80c24.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=969&id=ufe957093&margin=%5Bobject%20Object%5D&name=image.png&originHeight=969&originWidth=1935&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1001890&status=done&style=none&taskId=u3566557e-3cc0-46a5-af1e-ef2be11e1d4&title=&width=1935)

### 消费者组

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697702107-74abb7c6-cc10-4a74-a995-a15fd52cfaa5.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=756&id=uf3f50c48&margin=%5Bobject%20Object%5D&name=image.png&originHeight=756&originWidth=1876&originalType=binary&ratio=1&rotation=0&showTitle=false&size=986966&status=done&style=none&taskId=ucde8a7d1-aa7e-41e9-bc12-4a7a6869efd&title=&width=1876)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697780575-284ce81f-1161-4be9-b0bd-5ed2414127cb.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=972&id=uf2ef3018&margin=%5Bobject%20Object%5D&name=image.png&originHeight=972&originWidth=1928&originalType=binary&ratio=1&rotation=0&showTitle=false&size=915010&status=done&style=none&taskId=ua54b8c32-d838-4fc5-8c67-3bb6bca1708&title=&width=1928)

### 消费某一个主题
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697964455-98f7bce5-3d63-42c6-afb2-f668417b9868.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=541&id=u5748b96f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=541&originWidth=1383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=405215&status=done&style=none&taskId=u32628128-bb34-4dee-ab30-e638a616887&title=&width=1383)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650697991220-1c9d4870-e046-4079-b24f-c861f82382df.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=766&id=u3749fef5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=766&originWidth=1381&originalType=binary&ratio=1&rotation=0&showTitle=false&size=489819&status=done&style=none&taskId=u53247039-3275-459e-94fd-84b4ebee6e4&title=&width=1381)


### 消费某一个主题下特定分区
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650698085217-95aa5766-5789-4c0c-a6e0-1e6cbf5b381d.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=508&id=u6db2eb14&margin=%5Bobject%20Object%5D&name=image.png&originHeight=508&originWidth=1292&originalType=binary&ratio=1&rotation=0&showTitle=false&size=256571&status=done&style=none&taskId=u4061aac7-c3db-4c24-9819-01da9c4214b&title=&width=1292)




## Kafka-Eagle监控

---




## Kafka-Kraft模式

---



## SpringBoot

---

- 创建项目

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650698869747-22215d31-0e36-4dc0-8718-2611d9a22b4b.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=463&id=u8a361170&margin=%5Bobject%20Object%5D&name=image.png&originHeight=463&originWidth=1015&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183208&status=done&style=none&taskId=ud2397005-c04b-46fa-a1bb-a80f19633c5&title=&width=1015)

- 生产者

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650698963898-5c1fae9b-6f26-4770-8fb4-832aef835456.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=488&id=ucce8b6a2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=488&originWidth=652&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187841&status=done&style=none&taskId=ube47e302-beb5-4a64-bdfa-c645b2a89fd&title=&width=652)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650699127096-76fdbe7a-7c2e-4893-a0cc-7e551305e739.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=282&id=uc2b1ddf9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=282&originWidth=1245&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236784&status=done&style=none&taskId=u88c91899-76b2-4673-8846-53d1220a52a&title=&width=1245)

- 消费者

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650699223357-eebd5709-60b4-4294-88ea-72fa05167c78.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=341&id=u8110509d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=341&originWidth=721&originalType=binary&ratio=1&rotation=0&showTitle=false&size=157643&status=done&style=none&taskId=u5e278086-a105-4d5e-bebf-3b455fd0cb4&title=&width=721)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650699263675-b24b7fb5-c548-40b1-b810-385a2c799904.png#clientId=uf6a4b98f-a327-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=243&id=u4ed69fa6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=243&originWidth=1256&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175336&status=done&style=none&taskId=ufe6b881f-55cf-446c-95d8-10288a6db45&title=&width=1256)



## Kafka调优

---


