---


## 预备知识

---

### 日志实现

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651573989597-650b38da-72ea-425e-bf8e-4a626eb16285.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=485&id=u4e5362dd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=606&originWidth=1158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=215769&status=done&style=none&taskId=u392b3a54-b491-4fff-b87a-03aa05d276a&title=&width=926.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651574014296-076f6992-6e3c-4443-95a1-bcdc350223aa.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=542&id=ubc8b04e2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=677&originWidth=1158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=306035&status=done&style=none&taskId=u2b54c647-0ae1-4db7-a35f-7cd5c137a2f&title=&width=926.4)

## 进程和线程

---

### 进程与线程

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651574113358-6d6c930e-af74-46f7-a750-da504e24d775.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=341&id=uc901ab13&margin=%5Bobject%20Object%5D&name=image.png&originHeight=426&originWidth=1093&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153670&status=done&style=none&taskId=u0b8ded97-8ec6-45cc-bbc2-7c58cf26e0f&title=&width=874.4)
### 并发与并行

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651574307212-39728ff7-c208-4f9b-952a-fe79cc275082.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=138&id=u198a02ad&margin=%5Bobject%20Object%5D&name=image.png&originHeight=173&originWidth=798&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86305&status=done&style=none&taskId=uec7daf58-7341-42fd-a250-e1549013d72&title=&width=638.4)

### 异步与同步

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651574472931-602b1db7-4614-48c1-8a7c-3c0439bbc1ff.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=184&id=u084c9a74&margin=%5Bobject%20Object%5D&name=image.png&originHeight=230&originWidth=868&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62821&status=done&style=none&taskId=u3bc6f8e3-cefe-4278-bcc1-ba57dce1d86&title=&width=694.4)
同步
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651574638406-ac9fcebd-568b-466f-9197-bbe84b54c64b.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=194&id=u94f0ffd3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=242&originWidth=655&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61595&status=done&style=none&taskId=u8f4a88d8-2a5d-471d-ac97-6a6ddffce82&title=&width=524)
异步
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651574607780-f32a821a-9023-479b-93cb-f286add58bbe.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=403&id=u19210f4b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=504&originWidth=1192&originalType=binary&ratio=1&rotation=0&showTitle=false&size=226777&status=done&style=none&taskId=u36a1ccc8-be49-46a4-ae06-8588b88c428&title=&width=953.6)

### 多核多线程与单核多线程

---

只有多核多线程才能提升效率
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651575025495-09e1a457-61dc-4224-84cd-325372ef6b7e.png#clientId=ue3d72458-cf0c-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=285&id=ueeb0a651&margin=%5Bobject%20Object%5D&name=image.png&originHeight=356&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=210282&status=done&style=none&taskId=ub0c0b47a-ba81-49b1-bb37-748be1e0b35&title=&width=951.2)


## Java线程

---


### 1_直接使用Thread

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651675255398-f250f43a-d2ba-49d0-aa3d-4bb67f3ad9db.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=273&id=ua766b453&margin=%5Bobject%20Object%5D&name=image.png&originHeight=341&originWidth=1148&originalType=binary&ratio=1&rotation=0&showTitle=false&size=98732&status=done&style=none&taskId=ud0839ed4-9ba6-42ff-a991-b655a59bc76&title=&width=918.4)
本质是子类覆盖了父类的run方法

### 2_Runnable实现

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651675417271-52fb4c49-4c15-409b-897b-79fcd14879a3.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=265&id=uf5345b7f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=331&originWidth=1145&originalType=binary&ratio=1&rotation=0&showTitle=false&size=79565&status=done&style=none&taskId=u1c5860b6-3f15-4cff-ac59-1a5e57fdd90&title=&width=916)
只有一个抽象方法，会加上@FunctionalInterface, 可以使用lambda表达式
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651675587811-45cf5d3b-4f8e-496f-8cde-fa0361131e4d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=70&id=u88f3f647&margin=%5Bobject%20Object%5D&name=image.png&originHeight=88&originWidth=653&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32825&status=done&style=none&taskId=u2236af78-e51f-4b8b-831f-e2637a2f1ee&title=&width=522.4)


### 3_FutureTask实现

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651675782008-95d07cbc-6e87-4970-8e7b-671cbe0ee418.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=392&id=u3aa874b8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=490&originWidth=1174&originalType=binary&ratio=1&rotation=0&showTitle=false&size=147899&status=done&style=none&taskId=u50c2a846-98de-4adf-b958-79f93718b30&title=&width=939.2)


### 查看进程线程方法

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651676320776-47787a15-b517-43e0-98cd-cd067dcc8f6a.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=672&id=ue4b53605&margin=%5Bobject%20Object%5D&name=image.png&originHeight=840&originWidth=842&originalType=binary&ratio=1&rotation=0&showTitle=false&size=131197&status=done&style=none&taskId=u7fedb0d2-178b-42c6-8975-155df5f6a3f&title=&width=673.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651676360690-bebd3da7-7f13-4174-bcf8-0af883c5204e.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=659&id=u478926db&margin=%5Bobject%20Object%5D&name=image.png&originHeight=824&originWidth=1201&originalType=binary&ratio=1&rotation=0&showTitle=false&size=201654&status=done&style=none&taskId=u969ad4ea-a975-482a-9226-b6ae6e1db8c&title=&width=960.8)


### 栈和栈帧

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651676594239-e9c8867e-9e0d-475a-9e5e-f2a4d2e393b1.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=612&id=u0722a858&margin=%5Bobject%20Object%5D&name=image.png&originHeight=765&originWidth=1290&originalType=binary&ratio=1&rotation=0&showTitle=false&size=324448&status=done&style=none&taskId=u996e9c56-49bd-4197-bbeb-81386604c19&title=&width=1032)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651676830145-eb2ad1b0-60dd-455e-a7af-30a05bd9bf12.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=526&id=ud8c7c44c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=657&originWidth=1165&originalType=binary&ratio=1&rotation=0&showTitle=false&size=483124&status=done&style=none&taskId=u97b59c41-39ee-4924-beef-e7e29690e63&title=&width=932)

### 线程的上下文切换

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651676970230-defdee58-4861-4ad6-b892-cb153a5208a3.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=391&id=u7696f9f2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=489&originWidth=1172&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175804&status=done&style=none&taskId=u1b807ee6-e1e4-4a65-aceb-a5e8927031c&title=&width=937.6)
### 
### 
### 常见方法

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651677164175-1689e0eb-d796-40c3-9c37-348635562941.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=683&id=ub97ff2aa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=854&originWidth=1242&originalType=binary&ratio=1&rotation=0&showTitle=false&size=304375&status=done&style=none&taskId=u432809ac-3754-42a7-8a1c-485443459c9&title=&width=993.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651677301457-413b70e2-3da4-49bb-a6b1-e98078fffb5e.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=585&id=ua8cc5550&margin=%5Bobject%20Object%5D&name=image.png&originHeight=731&originWidth=1148&originalType=binary&ratio=1&rotation=0&showTitle=false&size=209450&status=done&style=none&taskId=u6d3948c2-1ac7-4108-b24a-28bea9f02bb&title=&width=918.4)

### start 和 run 方法

---

run不会启动新的线程，start才会启动新的线程


### Sleep 和 yield方法

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651677541984-e6398ac3-fc93-4761-a809-6d9021e2b1f5.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=401&id=u3fa880ca&margin=%5Bobject%20Object%5D&name=image.png&originHeight=501&originWidth=1199&originalType=binary&ratio=1&rotation=0&showTitle=false&size=163184&status=done&style=none&taskId=u86bc94f8-b68e-4e98-8cdd-ede4a9b708f&title=&width=959.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651677654321-e71751d1-1e97-470d-afd0-6a5d338df77e.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=439&id=u6dc3a299&margin=%5Bobject%20Object%5D&name=image.png&originHeight=549&originWidth=834&originalType=binary&ratio=1&rotation=0&showTitle=false&size=146088&status=done&style=none&taskId=u64e2ee04-f0bd-4e29-9033-3af95426d22&title=&width=667.2)


### join方法

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651678079081-b516656c-e01e-4952-a618-fdd2dca2579b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=394&id=uff6eb0bb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=493&originWidth=703&originalType=binary&ratio=1&rotation=0&showTitle=false&size=131162&status=done&style=none&taskId=uce51238b-b948-4123-9dc8-b1e36ec7ac6&title=&width=562.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651678108162-747e60f0-cca8-4bbb-bf8a-2859e40be684.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=599&id=u778c5265&margin=%5Bobject%20Object%5D&name=image.png&originHeight=749&originWidth=757&originalType=binary&ratio=1&rotation=0&showTitle=false&size=82647&status=done&style=none&taskId=u54b31d5e-b866-47ed-b259-c3496e445ee&title=&width=605.6)

### interrupt方法

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651678316228-6c0935db-8638-4c9b-b905-0aaeb3a39465.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=440&id=uda459074&margin=%5Bobject%20Object%5D&name=image.png&originHeight=550&originWidth=1165&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109318&status=done&style=none&taskId=u5b37c33f-e6d7-4492-9b38-0f1d58bd41c&title=&width=932)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651678412518-9f5dcc7e-c145-43a1-afe5-a3604dd1448b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=601&id=u74d504fb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=751&originWidth=1163&originalType=binary&ratio=1&rotation=0&showTitle=false&size=145339&status=done&style=none&taskId=u54700058-abd2-4469-b853-9b386bb3c34&title=&width=930.4)

### 两阶段终止模式

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651714917795-2e9f386a-b9cd-4547-b31b-0a6584c5e47a.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=506&id=u451a2254&margin=%5Bobject%20Object%5D&name=image.png&originHeight=632&originWidth=971&originalType=binary&ratio=1&rotation=0&showTitle=false&size=157993&status=done&style=none&taskId=u1cebf84b-8306-4649-ad69-cbbb667337f&title=&width=776.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651715062019-f9dac1bb-7e81-488b-b0fc-33ef2f29cd59.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=513&id=u0ff0c849&margin=%5Bobject%20Object%5D&name=image.png&originHeight=641&originWidth=811&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89197&status=done&style=none&taskId=u8fcc4511-4bd4-4cf1-bb88-fd40aaa212b&title=&width=648.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651715273217-acf095ff-ef4f-48bb-b482-4cbc997bb041.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=663&id=ud44c2ed0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=829&originWidth=594&originalType=binary&ratio=1&rotation=0&showTitle=false&size=215754&status=done&style=none&taskId=ufa089fec-ed6f-42c6-8b82-3e9d70ea8e0&title=&width=475.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651715412241-8dea83fa-a1f9-454d-948a-4fdc88b2d70f.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=230&id=u176936a2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=288&originWidth=745&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86507&status=done&style=none&taskId=u6087b9b4-1460-4a9f-9f4b-a50d2fbe2b0&title=&width=596)

### 打断park线程

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651716097986-08a33889-4de7-45c9-bfb3-f459793b0c20.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=439&id=u8c4b5fe7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=549&originWidth=805&originalType=binary&ratio=1&rotation=0&showTitle=false&size=150576&status=done&style=none&taskId=ucde93327-0404-4f2b-9e1e-f1a90326e2e&title=&width=644)


### 守护线程

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651716761933-3a8f067a-70cc-4fd1-8615-22ac983bbbee.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=473&id=u49216d56&margin=%5Bobject%20Object%5D&name=image.png&originHeight=591&originWidth=1215&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234642&status=done&style=none&taskId=u775e5370-6a94-489f-b4d1-10e207f3027&title=&width=972)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651716836535-761c488e-3803-4bf6-9a66-40ff3415b409.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=350&id=ub920a792&margin=%5Bobject%20Object%5D&name=image.png&originHeight=437&originWidth=1187&originalType=binary&ratio=1&rotation=0&showTitle=false&size=138006&status=done&style=none&taskId=uf23accd9-a855-437e-a5e6-d171cf3216a&title=&width=949.6)

### 线程的五种状态

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651716940729-03173b1e-2e03-4410-a903-b20954d54567.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=566&id=u7fbe6292&margin=%5Bobject%20Object%5D&name=image.png&originHeight=708&originWidth=1109&originalType=binary&ratio=1&rotation=0&showTitle=false&size=223484&status=done&style=none&taskId=uf3dea863-23de-4da9-85d8-19c3d3fe247&title=&width=887.2)


### 线程的六种状态

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717130580-924fb3d1-0955-4d44-889f-d8fdaf69903a.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=616&id=u3fa92932&margin=%5Bobject%20Object%5D&name=image.png&originHeight=770&originWidth=1091&originalType=binary&ratio=1&rotation=0&showTitle=false&size=294261&status=done&style=none&taskId=u8d258934-7fdc-412a-b440-cf93fe311fe&title=&width=872.8)
timed_waiting ---- 调用sleep
blocked----上锁
waiting ---join方法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717393566-b9a6da91-9071-4810-86f8-4a063aa42ff0.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=542&id=ua043a12c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=677&originWidth=757&originalType=binary&ratio=1&rotation=0&showTitle=false&size=146740&status=done&style=none&taskId=u8afbaa64-29d7-4962-9fd1-9b017c6963b&title=&width=605.6)

### 总结

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717454323-10360b47-8024-44ce-9b75-d1a4ee330a2c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=577&id=u975d9d30&margin=%5Bobject%20Object%5D&name=image.png&originHeight=721&originWidth=768&originalType=binary&ratio=1&rotation=0&showTitle=false&size=144234&status=done&style=none&taskId=ue201ea57-b073-4da7-82f1-689df29da25&title=&width=614.4)


## 有锁并发

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717538740-a9e63528-1686-4247-80d7-4c34fc8f8fd6.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=330&id=ue3691fc4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=412&originWidth=818&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39513&status=done&style=none&taskId=u24028b01-9a60-4a65-b1b8-7e79dcec674&title=&width=654.4)

### 共享问题

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717718296-6a868812-a50e-43d5-84e8-273e30d1ee0b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=565&id=u2f4292a0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=706&originWidth=1149&originalType=binary&ratio=1&rotation=0&showTitle=false&size=125287&status=done&style=none&taskId=uce4d0d8f-6c9c-407c-8e2a-6b241a250ee&title=&width=919.2)


### Synchronized

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717894685-26ddb012-e9b7-43ab-82f6-308b039589e7.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=530&id=u795673ef&margin=%5Bobject%20Object%5D&name=image.png&originHeight=663&originWidth=1231&originalType=binary&ratio=1&rotation=0&showTitle=false&size=241337&status=done&style=none&taskId=u4089dd33-4c0f-4463-8b0a-6270eab3be9&title=&width=984.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651717946842-2b13f30a-c207-4c31-abe1-43be65e2f123.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=745&id=u4351a84e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=931&originWidth=1165&originalType=binary&ratio=1&rotation=0&showTitle=false&size=174927&status=done&style=none&taskId=u43e74fb2-3956-4775-a91f-36065667e90&title=&width=932)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651718348555-71d0b503-ef3f-4540-86ef-0ed1291932d6.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=509&id=uc4657c0c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=636&originWidth=1916&originalType=binary&ratio=1&rotation=0&showTitle=false&size=585879&status=done&style=none&taskId=ud63994a9-97a9-4c2e-88b8-c92e9143227&title=&width=1532.8)
成员方法锁住this
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651718546222-7adff459-10fd-4453-91df-04861973064b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=390&id=ufae920f5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=488&originWidth=1146&originalType=binary&ratio=1&rotation=0&showTitle=false&size=80636&status=done&style=none&taskId=u7aa9c9ea-1da8-4196-a369-952f2857139&title=&width=916.8)
静态方法锁住class
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651718605551-c98ba747-bb7f-4415-8617-2ec2f35c5d77.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=373&id=udfe7f6ff&margin=%5Bobject%20Object%5D&name=image.png&originHeight=466&originWidth=1138&originalType=binary&ratio=1&rotation=0&showTitle=false&size=90592&status=done&style=none&taskId=uadc0cef0-bec1-42ef-a077-c790d50e695&title=&width=910.4)

线程8锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651718757397-f7746aee-f2bd-4236-9aac-acb9a8b17aea.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=654&id=u53daf3ef&margin=%5Bobject%20Object%5D&name=image.png&originHeight=818&originWidth=729&originalType=binary&ratio=1&rotation=0&showTitle=false&size=222444&status=done&style=none&taskId=u20e207c4-8803-4fd0-94bd-028aed210de&title=&width=583.2)

### 变量线程安全分析

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651718887437-ea1fdcaf-0035-4351-8bba-12eadec49cec.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=503&id=u74f6fd87&margin=%5Bobject%20Object%5D&name=image.png&originHeight=629&originWidth=942&originalType=binary&ratio=1&rotation=0&showTitle=false&size=171656&status=done&style=none&taskId=uba9d9bb9-960d-4597-b141-460fe149c66&title=&width=753.6)
Arraylist线程不安全
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719026701-59cb409f-435c-42f8-9330-f18a41922fcb.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=518&id=ua2088f2e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=648&originWidth=704&originalType=binary&ratio=1&rotation=0&showTitle=false&size=257529&status=done&style=none&taskId=u285dfe7b-ef6f-4de2-b371-a5b09497c63&title=&width=563.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719044584-ad2eb522-a08c-413b-927b-913a75827f2a.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=590&id=u52789e08&margin=%5Bobject%20Object%5D&name=image.png&originHeight=738&originWidth=943&originalType=binary&ratio=1&rotation=0&showTitle=false&size=458730&status=done&style=none&taskId=u5676e66e-10da-488e-bc03-78815c35942&title=&width=754.4)
局部变量
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719308218-31034b65-2e63-4dc2-8cb4-70633fe7cbb4.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=288&id=ua88fcb7d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=360&originWidth=693&originalType=binary&ratio=1&rotation=0&showTitle=false&size=144456&status=done&style=none&taskId=u3e22d2df-d4dc-49dd-a843-664733e278f&title=&width=554.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719350648-0fcffe6c-37b5-4c5a-8cfc-39a77caf4948.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=590&id=udf824efd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=738&originWidth=923&originalType=binary&ratio=1&rotation=0&showTitle=false&size=487791&status=done&style=none&taskId=u68ab9424-a92a-4bbb-8361-d2005e7b983&title=&width=738.4)
暴露局部变量（线程不安全）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719506577-a07bbccb-4c28-4abc-b73d-d8aebee6ab2b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=718&id=udad95e74&margin=%5Bobject%20Object%5D&name=image.png&originHeight=897&originWidth=1168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=249869&status=done&style=none&taskId=ud4b8629a-5bd8-4689-a906-4597827708b&title=&width=934.4)

修改主类方法访问修饰符为private（线程安全，开闭原则的闭）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719619348-f5b93290-5c49-4639-b841-7e85d6f0744d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=647&id=u24d6762c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=809&originWidth=1092&originalType=binary&ratio=1&rotation=0&showTitle=false&size=206988&status=done&style=none&taskId=ub97a70ff-afc1-4217-ac51-4ad2378b413&title=&width=873.6)


### 常见线程安全类

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719676631-ab200efb-fc81-45ae-a3a6-ec8aa61f21c9.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=473&id=uf8a24925&margin=%5Bobject%20Object%5D&name=image.png&originHeight=591&originWidth=1202&originalType=binary&ratio=1&rotation=0&showTitle=false&size=117332&status=done&style=none&taskId=u5a21d5c7-9926-4974-8524-2baa3fd4081&title=&width=961.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719746661-2d2f7d96-da04-4488-96d5-2c6bac53c818.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=266&id=u5ee7f06e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=332&originWidth=1156&originalType=binary&ratio=1&rotation=0&showTitle=false&size=67602&status=done&style=none&taskId=u1d2aee95-530f-4883-8222-52627f711b6&title=&width=924.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719815883-4bbc056c-4ac8-46c0-8683-2c53113f2f25.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=642&id=u9c73b39a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=803&originWidth=1223&originalType=binary&ratio=1&rotation=0&showTitle=false&size=149235&status=done&style=none&taskId=u29ba9207-d193-46a8-88d2-70756e0e263&title=&width=978.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651719870382-dd80dc64-cc50-491e-a361-ee24af00a5d6.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=506&id=ua79f7929&margin=%5Bobject%20Object%5D&name=image.png&originHeight=632&originWidth=1196&originalType=binary&ratio=1&rotation=0&showTitle=false&size=156325&status=done&style=none&taskId=uae1fc73b-b2ac-41d4-b385-38f159b0c3f&title=&width=956.8)

### Monitor（锁）概念

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651720187794-91dc034e-0cf7-4315-a385-9248c3d0ba94.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=670&id=u686d4bcf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=838&originWidth=1186&originalType=binary&ratio=1&rotation=0&showTitle=false&size=358990&status=done&style=none&taskId=ub62b62ff-c8bc-482c-8ab7-43b655e6b63&title=&width=948.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651720243287-24624c64-0921-460c-9e1b-316d430f3ac1.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=409&id=u8377df8e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=511&originWidth=1174&originalType=binary&ratio=1&rotation=0&showTitle=false&size=213527&status=done&style=none&taskId=ued07b378-412c-41e1-887b-da63fae2f3c&title=&width=939.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651720295021-534e88b5-8a30-4317-bb8f-119da7c5d2ab.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=746&id=uf7b33b7c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=932&originWidth=1295&originalType=binary&ratio=1&rotation=0&showTitle=false&size=362401&status=done&style=none&taskId=u2ba24202-33d8-435d-88dd-93fccf328cf&title=&width=1036)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651720511961-99164e12-a0b8-4914-ab1d-eeeb74b5120c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=244&id=uc267d394&margin=%5Bobject%20Object%5D&name=image.png&originHeight=305&originWidth=1193&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94291&status=done&style=none&taskId=uc2c4d32c-3051-4c6f-b7cf-72a6cfed824&title=&width=954.4)


### 轻量级锁

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721019886-fffb18d8-7f0a-4f61-bc07-57b3de0ff8e4.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=558&id=udab30f34&margin=%5Bobject%20Object%5D&name=image.png&originHeight=698&originWidth=1231&originalType=binary&ratio=1&rotation=0&showTitle=false&size=178324&status=done&style=none&taskId=u4d6bcf18-e89d-477a-8df4-18556d23bf1&title=&width=984.8)
对象加锁的时候栈帧有一个锁记录，其中有一个头记录，为00，加锁时会与monitor中的头记录01交换
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721133650-420198af-ea41-4075-baca-75a81f546368.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=731&id=u27d6ff2a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=914&originWidth=1207&originalType=binary&ratio=1&rotation=0&showTitle=false&size=361459&status=done&style=none&taskId=u1528ce5e-8976-4dcf-9919-a12d27e83c3&title=&width=965.6)


### 锁膨胀

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721308149-29bee446-2783-450f-82e7-7c89bfabfc07.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=640&id=ua05ee93c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=800&originWidth=1236&originalType=binary&ratio=1&rotation=0&showTitle=false&size=507777&status=done&style=none&taskId=ud5247c0e-2318-4130-b011-b872b98e136&title=&width=988.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721387303-2b80078f-152c-4d9a-b005-f7154f6b2df0.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=442&id=u319b189d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=553&originWidth=1164&originalType=binary&ratio=1&rotation=0&showTitle=false&size=432503&status=done&style=none&taskId=u1859e849-1a4a-40f2-ad9b-88a1735b856&title=&width=931.2)

### 自旋优化

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721457467-0fbf4b8d-ff28-4f78-9513-a12684da3854.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=114&id=ua05de94e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=143&originWidth=1178&originalType=binary&ratio=1&rotation=0&showTitle=false&size=85380&status=done&style=none&taskId=uf37347a5-f939-4c7e-afe2-4679925a906&title=&width=942.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721479305-2b55d509-4ea9-4ad0-b84c-6def576e68be.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=526&id=u7418f0f4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=657&originWidth=1183&originalType=binary&ratio=1&rotation=0&showTitle=false&size=210275&status=done&style=none&taskId=u02eeef08-aff4-42d1-9337-1787422b98b&title=&width=946.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721499106-1b3efe70-e2dc-47e9-b930-d188714771ec.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=500&id=u67c1114c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=625&originWidth=1158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=208743&status=done&style=none&taskId=ud6c8afa2-a507-4f79-92cd-4e006471d3a&title=&width=926.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721521554-8384c4c6-14b8-4b5b-9aa7-2932cb838aed.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=168&id=u47da62db&margin=%5Bobject%20Object%5D&name=image.png&originHeight=210&originWidth=1218&originalType=binary&ratio=1&rotation=0&showTitle=false&size=120096&status=done&style=none&taskId=u5ba1070f-d125-4520-a7f1-3af4f693c7d&title=&width=974.4)

### 偏向锁

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721554908-fb650275-31a4-4675-93af-94002473fe9d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=682&id=u2336431d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=853&originWidth=1210&originalType=binary&ratio=1&rotation=0&showTitle=false&size=249551&status=done&style=none&taskId=u9d15a6f3-ac08-4b49-9ea5-e35af5bfd41&title=&width=968)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721651016-4737ea2f-1527-49c4-bc8d-f91d4687a78d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=742&id=uceac40ba&margin=%5Bobject%20Object%5D&name=image.png&originHeight=928&originWidth=1003&originalType=binary&ratio=1&rotation=0&showTitle=false&size=285861&status=done&style=none&taskId=u5deb283f-4bf6-4571-b82d-71ef63e1c57&title=&width=802.4)


### 锁消除

---

JIT即时编译器进行锁优化
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651721917869-452ad42c-8ad2-4f0b-b8f8-84426d0641c9.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=322&id=u26993139&margin=%5Bobject%20Object%5D&name=image.png&originHeight=402&originWidth=1162&originalType=binary&ratio=1&rotation=0&showTitle=false&size=102996&status=done&style=none&taskId=ufbf8a6f3-ec22-4f5f-80dd-282e16fe6e3&title=&width=929.6)



### Wait 和 notify

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651722018681-996ff614-3416-4fea-bfd9-e94c4996f38c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=763&id=ubeb31f8d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=954&originWidth=1138&originalType=binary&ratio=1&rotation=0&showTitle=false&size=465427&status=done&style=none&taskId=ud61b4676-8c31-4862-a399-fb395a0c5ba&title=&width=910.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651722039384-8f5581db-b996-4c4b-95e6-55b761077f18.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=561&id=u94250f1f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=701&originWidth=1147&originalType=binary&ratio=1&rotation=0&showTitle=false&size=357955&status=done&style=none&taskId=u46120e3e-ce6b-4ff7-bf23-e28fa69a515&title=&width=917.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651722074791-81af20bb-f376-4603-9185-de770c9dc04f.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=696&id=ub87b6a64&margin=%5Bobject%20Object%5D&name=image.png&originHeight=870&originWidth=1216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263952&status=done&style=none&taskId=u7ef930a9-f0a9-4a91-adda-3c03425fc5a&title=&width=972.8)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651722208752-336dbb46-ef62-4395-a24b-a3c0e4dc58a2.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=174&id=uc26f2259&margin=%5Bobject%20Object%5D&name=image.png&originHeight=218&originWidth=981&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78221&status=done&style=none&taskId=u95ed1665-87f4-4dd5-b758-faf133d9d1b&title=&width=784.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651722294221-35df134c-2e05-4fc5-b065-66e9e5a584b5.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=478&id=u86020f32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=597&originWidth=503&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183498&status=done&style=none&taskId=u79ec153d-0377-479d-a3ba-5624cb55e07&title=&width=402.4)


### 同步模式之保护性暂停

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651724196000-687d7147-8f10-4313-9605-5d32c8cc6806.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=567&id=ua1de8145&margin=%5Bobject%20Object%5D&name=image.png&originHeight=709&originWidth=1105&originalType=binary&ratio=1&rotation=0&showTitle=false&size=265422&status=done&style=none&taskId=u1e91ab30-0a9e-4978-aa32-2f571595f4a&title=&width=884)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651724319299-62e7af27-6cda-49e8-bfa4-b386ce5492b5.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=595&id=u71f19e8d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=744&originWidth=591&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155545&status=done&style=none&taskId=ubff79935-0e84-4b24-b36d-ec85411e94d&title=&width=472.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651724464110-85976e05-bebb-44f8-8c24-86a008dab5c9.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=498&id=u650ad26a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=623&originWidth=716&originalType=binary&ratio=1&rotation=0&showTitle=false&size=228933&status=done&style=none&taskId=u41550d01-a96e-4adc-b218-a7c5e27d3b9&title=&width=572.8)
增加超时效果
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651724730827-25e41581-4cf1-4f64-9189-e09922365bda.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=626&id=u443a9a02&margin=%5Bobject%20Object%5D&name=image.png&originHeight=782&originWidth=876&originalType=binary&ratio=1&rotation=0&showTitle=false&size=269068&status=done&style=none&taskId=u5cfeb2f7-6fdc-46d6-b4c4-d4a49309627&title=&width=700.8)


### 异步模式之生产者/消费者

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651724949068-0179d9c9-8db1-4309-9d37-6b9a4e6d3836.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=479&id=u4ddf1a83&margin=%5Bobject%20Object%5D&name=image.png&originHeight=599&originWidth=1199&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274548&status=done&style=none&taskId=u3c74b474-f9e5-435c-9749-97f33e4a7ea&title=&width=959.2)

### 多把锁

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651725235307-6622d5bc-9148-43a6-9663-a7053a8ee27d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=684&id=uaedab5d2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=855&originWidth=629&originalType=binary&ratio=1&rotation=0&showTitle=false&size=240796&status=done&style=none&taskId=u6b1efa4a-a1c0-4dfb-b6a8-451a0018aea&title=&width=503.2)

### 活跃性

---

死锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651725337361-ae909781-1118-45db-bd42-f00b51827b30.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=610&id=u75a768c7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=762&originWidth=636&originalType=binary&ratio=1&rotation=0&showTitle=false&size=198510&status=done&style=none&taskId=u3806b363-f162-482b-9c01-6d2fffa18cd&title=&width=508.8)
定位死锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651725374278-10282708-12d1-45ac-a698-4d393ce924fb.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=702&id=u745c052b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=877&originWidth=1187&originalType=binary&ratio=1&rotation=0&showTitle=false&size=374185&status=done&style=none&taskId=u8005b670-ac5e-4d72-9566-51f094bdbf3&title=&width=949.6)

活锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651725538899-29251622-1e61-4edc-8519-1310d4a5ddfe.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=557&id=u05eb4c0a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=696&originWidth=530&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217810&status=done&style=none&taskId=u16fd774f-9a9c-4a0d-afc2-9d5028f07b6&title=&width=424)
饥饿问题



### ReentrantLock

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651725616345-b5decfec-ca6c-4971-bcf5-286e44787e26.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=272&id=u1313fe0a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=340&originWidth=1160&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56620&status=done&style=none&taskId=u0bc5aae4-e25c-4bb2-9e2f-8be6fed9a1d&title=&width=928)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651725693375-f07ddda4-cc32-4e2a-9140-50a3a3eaa9cb.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=300&id=u2b5e7d10&margin=%5Bobject%20Object%5D&name=image.png&originHeight=375&originWidth=1181&originalType=binary&ratio=1&rotation=0&showTitle=false&size=60113&status=done&style=none&taskId=u7a7cf4e0-8a82-454e-a851-17f0a84e18f&title=&width=944.8)

可打断
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726059484-d3570303-d4dd-4146-8c2d-611ea9fac06a.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=471&id=u84691e7e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=589&originWidth=560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=163440&status=done&style=none&taskId=ue312d106-42dc-405d-8704-74bdcfc0c1b&title=&width=448)
锁超时
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726150233-b431ccb6-4b9d-4e00-a53b-d142f0a3235c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=486&id=u0518fb36&margin=%5Bobject%20Object%5D&name=image.png&originHeight=607&originWidth=881&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216623&status=done&style=none&taskId=u1134ade9-0720-4cc8-a86c-3d13abee270&title=&width=704.8)

公平锁
会按照等待队列顺序来

条件变量
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726242077-dd08c1e0-c810-4d44-8584-1ba17d0acc99.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=418&id=ubb46c994&margin=%5Bobject%20Object%5D&name=image.png&originHeight=522&originWidth=1220&originalType=binary&ratio=1&rotation=0&showTitle=false&size=180879&status=done&style=none&taskId=u29ddd070-4b2c-484e-84fc-f874deac508&title=&width=976)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726385271-ff6d0602-d40c-4251-a711-bc52a14cbd6c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=691&id=u6f4b0657&margin=%5Bobject%20Object%5D&name=image.png&originHeight=864&originWidth=738&originalType=binary&ratio=1&rotation=0&showTitle=false&size=299941&status=done&style=none&taskId=ude09a40f-96b9-4dd3-84ba-eef105d26ca&title=&width=590.4)



### 同步--固定运行顺序

---

wait-notify
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726520208-88216844-c526-4e62-acd6-ddf9d87eb4d3.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=635&id=uf5abd62c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=794&originWidth=685&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234616&status=done&style=none&taskId=u39dbe0a3-21d1-492b-8f31-50c9a1b15c7&title=&width=548)


awaite和signal（与上述类似）

park 和 unpark
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726647059-6b59bec1-d4bc-4761-ac3e-2859fb9c40b2.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=366&id=u8324efa9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=458&originWidth=538&originalType=binary&ratio=1&rotation=0&showTitle=false&size=126784&status=done&style=none&taskId=u5ca495c0-05a2-4293-8838-1f22a47014c&title=&width=430.4)


### 同步--交替输出

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651726769709-35e98f09-7e03-48f3-bf3d-52135bdf9ac6.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=602&id=u41a0bd96&margin=%5Bobject%20Object%5D&name=image.png&originHeight=752&originWidth=727&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274575&status=done&style=none&taskId=ub2164cac-fcd3-4ceb-ba9d-5395d93e288&title=&width=581.6)


await 和 signal


park 和 unpark

### 总结

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727054034-7270ef37-c758-446a-87d6-f86385a4daa8.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=680&id=ub12f3a99&margin=%5Bobject%20Object%5D&name=image.png&originHeight=850&originWidth=882&originalType=binary&ratio=1&rotation=0&showTitle=false&size=243092&status=done&style=none&taskId=u28316512-b384-42c9-b653-e95a7967d08&title=&width=705.6)


## JMM-JAVA 内存模型

---

内存模型：
原子性
可见性
有序性

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727204948-e719f137-54cb-4930-af10-91644f5866f5.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=329&id=u1d1c22cb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=411&originWidth=1196&originalType=binary&ratio=1&rotation=0&showTitle=false&size=120007&status=done&style=none&taskId=u00ba0524-5097-49b5-b7b1-828239c2bc2&title=&width=956.8)

### 原子性

---

synchronized 加锁之后如果发生上下文切换，并不会释放锁，保证了原子性


### 可见性

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727507338-f72ccf05-abfc-4243-8356-d53f57b8ed1b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=348&id=u03a8019d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=435&originWidth=748&originalType=binary&ratio=1&rotation=0&showTitle=false&size=131776&status=done&style=none&taskId=ub1d58148-d9b1-4d00-aec9-37e73ccf917&title=&width=598.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727560888-a1e28ec2-0d6a-4434-9234-dd613d2e2d79.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=408&id=u55310219&margin=%5Bobject%20Object%5D&name=image.png&originHeight=510&originWidth=1193&originalType=binary&ratio=1&rotation=0&showTitle=false&size=225866&status=done&style=none&taskId=u26a52ae2-3501-4fa3-a4c3-a237d4462fc&title=&width=954.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727587793-2da42e4b-7b71-4c05-81bc-335ede063a80.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=377&id=u7acf8b77&margin=%5Bobject%20Object%5D&name=image.png&originHeight=471&originWidth=1187&originalType=binary&ratio=1&rotation=0&showTitle=false&size=240465&status=done&style=none&taskId=ue82aa595-f3e0-4e8d-8720-76cee46d9c8&title=&width=949.6)
解决方案：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727631090-7a156560-bdc5-448a-8a30-3fe478015819.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=395&id=udfea83df&margin=%5Bobject%20Object%5D&name=image.png&originHeight=494&originWidth=694&originalType=binary&ratio=1&rotation=0&showTitle=false&size=130331&status=done&style=none&taskId=u9941490d-6553-4383-a14a-4975afc521e&title=&width=555.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727652996-64dcd94c-a3f7-4fb9-9792-1883f8e3731c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=152&id=uf432738e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=190&originWidth=1173&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68148&status=done&style=none&taskId=ud1f4e254-ca54-4636-9ae7-92041c69cdf&title=&width=938.4)

synchronized解决
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727753725-ad584661-3123-4a77-9abe-85fda5c89d5d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=603&id=uc567d7cc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=754&originWidth=791&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197283&status=done&style=none&taskId=uceff994e-e811-409c-9660-15ab812a128&title=&width=632.8)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727816452-231a7279-09a2-4891-ac05-f63ca00b6361.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=370&id=u86810e76&margin=%5Bobject%20Object%5D&name=image.png&originHeight=463&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=152802&status=done&style=none&taskId=u162b781f-6d4e-4758-a655-ed9e691464f&title=&width=951.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651727832928-81bcbe54-cdd2-4a71-bbd4-e3bdcc31022d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=507&id=u10165a7b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=634&originWidth=1227&originalType=binary&ratio=1&rotation=0&showTitle=false&size=205718&status=done&style=none&taskId=u35e5726d-5ea4-46bd-8bad-0af6843fc6d&title=&width=981.6)


### 有序性

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728020120-ca1dced1-cf41-4d8f-bf5e-f55f6ba11767.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=648&id=u2eae8f73&margin=%5Bobject%20Object%5D&name=image.png&originHeight=810&originWidth=1172&originalType=binary&ratio=1&rotation=0&showTitle=false&size=173939&status=done&style=none&taskId=u2863f56b-43a8-4846-aabe-f59e78615dc&title=&width=937.6)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728108706-e047f86a-199a-4c0b-ada7-cb0094dad258.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=217&id=u466c604f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=271&originWidth=1155&originalType=binary&ratio=1&rotation=0&showTitle=false&size=139423&status=done&style=none&taskId=ua66a2223-4068-4166-80ab-fc78bf8c4af&title=&width=924)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728121436-9e497153-5988-4f17-a5bc-5b429438af87.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=321&id=u1966119d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=401&originWidth=1125&originalType=binary&ratio=1&rotation=0&showTitle=false&size=438277&status=done&style=none&taskId=ue2cf5184-66fa-4605-9523-8430f97855d&title=&width=900)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728150656-1c2459d7-0dd3-4130-93c5-303858056cd4.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=575&id=ue5c09972&margin=%5Bobject%20Object%5D&name=image.png&originHeight=719&originWidth=1249&originalType=binary&ratio=1&rotation=0&showTitle=false&size=420160&status=done&style=none&taskId=ue5cec0d9-e011-4e1c-bd04-4c05f2b0e13&title=&width=999.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728189866-104ae5c1-05b7-408e-9b1e-ca141e0c8447.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=428&id=u9e62ea1f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=535&originWidth=1221&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187145&status=done&style=none&taskId=u062977cc-7b39-476a-8cbb-9b9774a002c&title=&width=976.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728245966-0cbd5882-f384-47bd-8afd-d95b70415236.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=547&id=u83e7dcd4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=684&originWidth=1192&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135695&status=done&style=none&taskId=u3273b055-5a38-4e8f-8745-a617c4ee81a&title=&width=953.6)
解决方法--volitile
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728289454-8292f938-c2cf-455e-9485-a0249de48c0c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=447&id=u0d638f7e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=559&originWidth=668&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121166&status=done&style=none&taskId=u22485e39-079c-428d-8e2a-798f237cc80&title=&width=534.4)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728376564-b3dc0d54-f983-4987-bcab-d55995644a86.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=544&id=u2f730c77&margin=%5Bobject%20Object%5D&name=image.png&originHeight=680&originWidth=1211&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197202&status=done&style=none&taskId=u4dc5e1b5-742f-4e3c-85b5-af6de75ea46&title=&width=968.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728477815-521ff19c-ed67-4934-99da-f92f94eed2e3.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=505&id=u5fb9363c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=631&originWidth=1172&originalType=binary&ratio=1&rotation=0&showTitle=false&size=179629&status=done&style=none&taskId=ua8083540-ff92-4ec6-9370-0c2192d25be&title=&width=937.6)


### 小结

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728598609-513e5302-2afb-4db5-8813-6dc1b4caeb24.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=439&id=u6ee10591&margin=%5Bobject%20Object%5D&name=image.png&originHeight=549&originWidth=922&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96197&status=done&style=none&taskId=u5aa69bf1-9a8f-4493-88eb-4903c80d92b&title=&width=737.6)


## 无锁并发

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728707318-6a1aa591-93c1-44ed-a5f4-ee73e009626f.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=284&id=u6e22d624&margin=%5Bobject%20Object%5D&name=image.png&originHeight=355&originWidth=1114&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37220&status=done&style=none&taskId=uddb20199-d7d9-4930-9350-df7fb6692fd&title=&width=891.2)

### 保护共享资源

---

加锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728817213-dd7affbc-6798-4177-af2f-297e60b0ad93.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=477&id=u70ea9dc3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=596&originWidth=967&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155123&status=done&style=none&taskId=u6c5e3d23-1b46-4cbe-b4e4-0062a0b66a6&title=&width=773.6)
无锁
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651728948886-37e20418-8ab5-43a3-8415-7ab37a24b3cc.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=558&id=u9f659341&margin=%5Bobject%20Object%5D&name=image.png&originHeight=698&originWidth=774&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194452&status=done&style=none&taskId=u45663d62-535c-4fd3-bb56-6d3946f96ad&title=&width=619.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729232233-15d76f6c-b373-424a-8d18-0f2453430010.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=490&id=u04c85847&margin=%5Bobject%20Object%5D&name=image.png&originHeight=613&originWidth=1091&originalType=binary&ratio=1&rotation=0&showTitle=false&size=227314&status=done&style=none&taskId=u09859db3-5081-4d83-aec7-fb890b71037&title=&width=872.8)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729075166-92562ba2-42d6-444f-949e-9bcd1e09cd75.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=94&id=udf09adfc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=117&originWidth=1184&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33377&status=done&style=none&taskId=u1d89b410-d15a-49c6-8263-1e3d18b615f&title=&width=947.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729127874-7ababb78-6cd1-40cf-8f1b-61a98ca55155.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=614&id=u8f29fc91&margin=%5Bobject%20Object%5D&name=image.png&originHeight=767&originWidth=807&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109198&status=done&style=none&taskId=u27d52864-4e7a-496b-9617-99ddb9b73ee&title=&width=645.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729161983-d14872d1-606a-4a86-a234-4e2a28e6bb90.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=226&id=ucfe04080&margin=%5Bobject%20Object%5D&name=image.png&originHeight=282&originWidth=1121&originalType=binary&ratio=1&rotation=0&showTitle=false&size=108470&status=done&style=none&taskId=u9000433f-9bab-4bb1-a02f-b405982ad46&title=&width=896.8)


### CAS与volatile

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729290132-5393d416-796d-4f8b-a19f-ed0f3444c6f3.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=426&id=uf6711d07&margin=%5Bobject%20Object%5D&name=image.png&originHeight=533&originWidth=1224&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175176&status=done&style=none&taskId=u49c704f6-ff1e-470e-b7b0-ab93177aa03&title=&width=979.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729350706-3e6d83c1-d12d-4a37-abfe-19f3877f6e82.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=310&id=u593141a9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=387&originWidth=1220&originalType=binary&ratio=1&rotation=0&showTitle=false&size=205690&status=done&style=none&taskId=u8f61f136-7ed2-41a2-a55a-26166b14d8e&title=&width=976)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729384777-dc9bf6e7-84a2-4ec0-965e-3cf3a66173bb.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=394&id=ubab94e6c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=493&originWidth=1179&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187607&status=done&style=none&taskId=uccb31f0e-e803-4acc-94dd-533e746c8e3&title=&width=943.2)


### 原子整数

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729442892-7f126f5d-81e0-49c2-85e4-753999effb49.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=658&id=uaaef2385&margin=%5Bobject%20Object%5D&name=image.png&originHeight=823&originWidth=1006&originalType=binary&ratio=1&rotation=0&showTitle=false&size=269191&status=done&style=none&taskId=u2269cac3-6145-4274-8979-040dd166af8&title=&width=804.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729560135-f743c5f1-8b6c-4c53-914b-28423b4c5eb0.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=390&id=uce99d8a0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=487&originWidth=754&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135340&status=done&style=none&taskId=u0ac05570-e41b-4b85-83d3-6ecc29e844c&title=&width=603.2)

### 原子引用

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729608576-d06e69b3-316d-4cbf-9265-ec1f719d8912.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=678&id=ueee24114&margin=%5Bobject%20Object%5D&name=image.png&originHeight=848&originWidth=1185&originalType=binary&ratio=1&rotation=0&showTitle=false&size=249420&status=done&style=none&taskId=ud00e3a92-5a7e-4ce9-a793-a351e63d124&title=&width=948)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729672987-c79e9ad9-0b91-46b3-a901-7a448f6f7692.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=503&id=ub7ca2b69&margin=%5Bobject%20Object%5D&name=image.png&originHeight=629&originWidth=832&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216373&status=done&style=none&taskId=u5d4d92ed-f035-497d-b084-4ce33e32087&title=&width=665.6)


A-->B-->A问题
> 主线程无法感知其他线程对变量修改

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729828818-6d90a5e1-6f98-412a-8091-2fd7985e8519.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=471&id=uf5e9bbff&margin=%5Bobject%20Object%5D&name=image.png&originHeight=589&originWidth=867&originalType=binary&ratio=1&rotation=0&showTitle=false&size=276895&status=done&style=none&taskId=uee20d6d1-03d3-42e5-9e3d-b14dd8c9d23&title=&width=693.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729867841-02323192-5452-41f0-9905-66ca6b2d1b49.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=166&id=u6adbb16c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=207&originWidth=1203&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87394&status=done&style=none&taskId=u3dffc4e5-33f2-408b-bab7-fc302535122&title=&width=962.4)

### 原子数组

---


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729941114-ef796c2a-f9b1-44b0-aff7-bf832fa9099a.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=174&id=u0471585a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=217&originWidth=649&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62325&status=done&style=none&taskId=u644d2fa5-62a2-4add-80e2-9532a4b7289&title=&width=519.2)


### 字段更新器
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651729994017-9907e589-d4cb-47f0-b001-29dd60174cc5.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=275&id=uc7150899&margin=%5Bobject%20Object%5D&name=image.png&originHeight=344&originWidth=1219&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107042&status=done&style=none&taskId=u40ba7130-cf8d-45c7-b660-17d80a31008&title=&width=975.2)

### 原子累加器

---


### Unsafe

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730110230-207f0942-205d-4b41-ae73-434bb3f850a1.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=518&id=u12493741&margin=%5Bobject%20Object%5D&name=image.png&originHeight=647&originWidth=1203&originalType=binary&ratio=1&rotation=0&showTitle=false&size=228673&status=done&style=none&taskId=u457d4e76-351e-4864-a89d-bab6367a467&title=&width=962.4)

### 总结

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730170519-69c46793-2c91-4123-81c0-377f685d0dff.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=458&id=u7241a5ee&margin=%5Bobject%20Object%5D&name=image.png&originHeight=573&originWidth=919&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61180&status=done&style=none&taskId=uaa8a0c62-8f58-489b-a207-a3eaf126c77&title=&width=735.2)


## 不可变类

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730211921-6ddd94dd-a00b-46ab-a110-672f79063f86.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=181&id=u33efa924&margin=%5Bobject%20Object%5D&name=image.png&originHeight=226&originWidth=1210&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26345&status=done&style=none&taskId=uf922472f-9f7b-49d2-8b1e-5d65e1ca1fc&title=&width=968)

### 日期转换问题

---

多线程下报错
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730250819-f2e2022d-3a71-47ca-bff4-96874bc4f38e.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=347&id=ubb985760&margin=%5Bobject%20Object%5D&name=image.png&originHeight=434&originWidth=1157&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158769&status=done&style=none&taskId=u9b4174ea-c6b8-4abd-a0f2-e4537780246&title=&width=925.6)

锁解决
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730361411-295d968b-79c6-4694-93cf-993c1e25b84c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=366&id=ud49cf850&margin=%5Bobject%20Object%5D&name=image.png&originHeight=457&originWidth=820&originalType=binary&ratio=1&rotation=0&showTitle=false&size=165216&status=done&style=none&taskId=ub4086db4-1212-437b-8b5e-875185e128f&title=&width=656)

不可变类解决
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730445528-3da4301f-28e2-4620-b7cb-7720aa2e9ce8.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=191&id=u669b01a0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=239&originWidth=751&originalType=binary&ratio=1&rotation=0&showTitle=false&size=113461&status=done&style=none&taskId=u9ce76d35-5dc0-446e-b099-fefea11f138&title=&width=600.8)


### 不可变设计

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730530310-e1d30787-188e-40a7-bd0d-6f9b818745fd.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=365&id=uae06e924&margin=%5Bobject%20Object%5D&name=image.png&originHeight=456&originWidth=1178&originalType=binary&ratio=1&rotation=0&showTitle=false&size=160557&status=done&style=none&taskId=u774adeb1-eb25-4d75-89ed-cc02db5ffed&title=&width=942.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730543692-6de10ba5-1106-47db-a668-45b9f91684ab.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=204&id=u777b8442&margin=%5Bobject%20Object%5D&name=image.png&originHeight=255&originWidth=1129&originalType=binary&ratio=1&rotation=0&showTitle=false&size=79402&status=done&style=none&taskId=u1d3e8387-4dca-48ed-8158-87becabdfe2&title=&width=903.2)

### 享元模式

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730670499-efbc4632-efac-45aa-9fa0-f2226bcfb5c1.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=338&id=u0616eb43&margin=%5Bobject%20Object%5D&name=image.png&originHeight=422&originWidth=1213&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94744&status=done&style=none&taskId=u204963f6-b7cd-4e2a-849f-68a87e75bf2&title=&width=970.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730704000-311f476a-f123-448a-9c10-77d3eceb95d1.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=446&id=u6cbd4e69&margin=%5Bobject%20Object%5D&name=image.png&originHeight=558&originWidth=1226&originalType=binary&ratio=1&rotation=0&showTitle=false&size=196904&status=done&style=none&taskId=u02407059-3d90-4f42-98fc-101469c30aa&title=&width=980.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730728064-ca39cb11-cd3f-4243-a2b3-23ff7c4f059c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=218&id=u71f1b42e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=272&originWidth=758&originalType=binary&ratio=1&rotation=0&showTitle=false&size=82894&status=done&style=none&taskId=u62fb6135-7a0b-4a54-a12c-415f03b3e80&title=&width=606.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730753933-a1034d05-0abc-457b-ae41-d1bf92b28670.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=202&id=u191ec942&margin=%5Bobject%20Object%5D&name=image.png&originHeight=253&originWidth=993&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78852&status=done&style=none&taskId=udc2b3dd1-cb7c-401a-a9fc-f2cd7d2450b&title=&width=794.4)


### 连接池

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651730918536-d580cec2-ec18-4230-9401-4f2a5a2d928d.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=103&id=u7060bb52&margin=%5Bobject%20Object%5D&name=image.png&originHeight=129&originWidth=1163&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96188&status=done&style=none&taskId=u4798aa58-e870-4357-bd29-5711b492f20&title=&width=930.4)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651735421058-3c9ef6b0-304b-4951-8d7c-54566968779c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=511&id=ua60545bd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=639&originWidth=681&originalType=binary&ratio=1&rotation=0&showTitle=false&size=208968&status=done&style=none&taskId=ufdfa7ba1-b552-4050-a64b-4f78cdf5944&title=&width=544.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651735518714-c0584a65-d922-4f4c-a1a1-2c8ddc9f0c6f.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=460&id=u1fd1a340&margin=%5Bobject%20Object%5D&name=image.png&originHeight=575&originWidth=891&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153694&status=done&style=none&taskId=u109e927b-dc4a-4d8c-a90d-870d3d5b61b&title=&width=712.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651735643319-9e7d1f9a-0a5c-4c40-a31e-cf9f2ea96014.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=262&id=u2e3f6ac9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=327&originWidth=744&originalType=binary&ratio=1&rotation=0&showTitle=false&size=82154&status=done&style=none&taskId=u72d71aa3-fe13-42e0-9807-87f1fe7e30a&title=&width=595.2)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651735717808-75b1a40a-1554-4f41-ba72-13d5b81b4b60.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=343&id=u30bcaed9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=429&originWidth=741&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143617&status=done&style=none&taskId=ufedc0b6a-e6ce-43fe-9751-5a7d56b9575&title=&width=592.8)



## 并发工具

---


### 线程池

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651736451897-28cf273b-7059-464f-be15-936cd72a9268.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=340&id=u0f2548d3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=425&originWidth=879&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89177&status=done&style=none&taskId=u07677502-5543-4660-8cea-7de311f6539&title=&width=703.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651736720634-d83c6038-19dc-4b86-9bba-34330dd5f520.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=370&id=uf547c6cc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=462&originWidth=1216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136128&status=done&style=none&taskId=u52d959a4-22ae-4d5f-83ea-1cd51c84884&title=&width=972.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651736797010-e2a718af-4019-4fb6-9108-d8a4feb41342.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=659&id=ucfb51598&margin=%5Bobject%20Object%5D&name=image.png&originHeight=824&originWidth=1202&originalType=binary&ratio=1&rotation=0&showTitle=false&size=329104&status=done&style=none&taskId=u1de24622-91e0-493f-80f4-84d37501d1b&title=&width=961.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651736819467-3a28a34d-ed71-4ee3-b4bf-661796760b35.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=554&id=ud2922127&margin=%5Bobject%20Object%5D&name=image.png&originHeight=693&originWidth=1227&originalType=binary&ratio=1&rotation=0&showTitle=false&size=164220&status=done&style=none&taskId=u20fc233e-44e2-49ab-9716-629a0fd410c&title=&width=981.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651736925195-2a5559ba-82a6-4e58-b9ce-f7ad79a99388.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=607&id=u5bb9d127&margin=%5Bobject%20Object%5D&name=image.png&originHeight=759&originWidth=448&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99397&status=done&style=none&taskId=uc6811552-5b99-4bff-a11b-eac938e8c0e&title=&width=358.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737337175-f12238f8-97ca-4aac-bf5f-67712a0f97fe.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=678&id=u057e56dd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=847&originWidth=737&originalType=binary&ratio=1&rotation=0&showTitle=false&size=108472&status=done&style=none&taskId=u05e85e22-0993-4c37-a6f3-fa6c9b29ee5&title=&width=589.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737496249-8cd435de-0049-4836-b3cf-2363c0406b84.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=646&id=u67c917aa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=807&originWidth=1220&originalType=binary&ratio=1&rotation=0&showTitle=false&size=413713&status=done&style=none&taskId=uab482eb5-6146-433c-a667-34944a23507&title=&width=976)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737651108-db1c709e-5e96-44e4-9415-4dfe4959e4a9.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=704&id=ud4550566&margin=%5Bobject%20Object%5D&name=image.png&originHeight=880&originWidth=1229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=241592&status=done&style=none&taskId=u821d4d37-6ac5-47c2-b58c-0d2d69d91c3&title=&width=983.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737930671-7e5f7455-5036-41f2-bd06-ab8201aa3529.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=191&id=u38736f93&margin=%5Bobject%20Object%5D&name=image.png&originHeight=239&originWidth=1174&originalType=binary&ratio=1&rotation=0&showTitle=false&size=60459&status=done&style=none&taskId=u3c10413c-e1d9-491f-bd77-238b5d34f72&title=&width=939.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737950154-065b7abe-7615-4f6b-a677-6414d5b67edd.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=687&id=u06fe4334&margin=%5Bobject%20Object%5D&name=image.png&originHeight=859&originWidth=1268&originalType=binary&ratio=1&rotation=0&showTitle=false&size=286665&status=done&style=none&taskId=u0dd0783b-93cc-48c5-b2de-29580fb5a9d&title=&width=1014.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651738079301-ba2b63df-8761-4df7-afd2-10cfc0e67dd3.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=701&id=u23b0e3ab&margin=%5Bobject%20Object%5D&name=image.png&originHeight=876&originWidth=1161&originalType=binary&ratio=1&rotation=0&showTitle=false&size=430447&status=done&style=none&taskId=u6dfe36ab-cc3d-424d-a9b6-0d28361d1e2&title=&width=928.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737706977-ad4ab5b9-a468-4a99-937a-e8e99a67603e.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=366&id=u94ff4cd0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=458&originWidth=719&originalType=binary&ratio=1&rotation=0&showTitle=false&size=134676&status=done&style=none&taskId=u4bbb2056-2081-44ec-a4bc-961e05fff91&title=&width=575.2)
给线程一个名称
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651737834384-e89cc6fa-b811-4fc2-a718-ae1d054b4ea6.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=366&id=u089aab31&margin=%5Bobject%20Object%5D&name=image.png&originHeight=457&originWidth=983&originalType=binary&ratio=1&rotation=0&showTitle=false&size=203088&status=done&style=none&taskId=ub78eb3ac-b529-42ae-9c05-a12278e52a1&title=&width=786.4)


### tomcat线程池

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651738488806-4a237152-4b22-4711-baf0-2c2d3507126c.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=222&id=u793aba45&margin=%5Bobject%20Object%5D&name=image.png&originHeight=277&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=98140&status=done&style=none&taskId=ua0541307-6119-41c9-b02e-ee553ffe976&title=&width=907.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651738538065-7c314b73-73f5-4029-8d6b-93f8ed117788.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=204&id=u59e1ff49&margin=%5Bobject%20Object%5D&name=image.png&originHeight=255&originWidth=1152&originalType=binary&ratio=1&rotation=0&showTitle=false&size=100975&status=done&style=none&taskId=u4b003248-5ffd-4d07-96e4-39795f8bea3&title=&width=921.6)



### AQS原理

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651738646670-98e9ff19-ad53-494b-b15c-24a9fa1b88bc.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=594&id=u5f8e3fbc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=742&originWidth=1235&originalType=binary&ratio=1&rotation=0&showTitle=false&size=212061&status=done&style=none&taskId=udf5f3d17-16d9-41ad-bcd7-d02fa0e539a&title=&width=988)


### ReentrantLock

---


...

### 线程安全集合类

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651738950260-a041184e-19d6-43e3-85ec-4b3dfb88639b.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=174&id=u619d9697&margin=%5Bobject%20Object%5D&name=image.png&originHeight=218&originWidth=1168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72898&status=done&style=none&taskId=ue59a18d5-1a88-4a94-bde3-3640da1a834&title=&width=934.4)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651739004340-b0fd156c-9bb8-41cb-b6d3-2bcb2774d678.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=482&id=u1a1adecd&margin=%5Bobject%20Object%5D&name=image.png&originHeight=603&originWidth=1163&originalType=binary&ratio=1&rotation=0&showTitle=false&size=131103&status=done&style=none&taskId=uf0ab2d52-d7c6-4dfc-b85e-fb73c8c4394&title=&width=930.4)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651739030062-fcf23a07-abd4-4fe7-a445-038561dd1820.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=492&id=u071c313c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=615&originWidth=1251&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216018&status=done&style=none&taskId=uce14f866-bddd-4e9e-9092-2dedddb0538&title=&width=1000.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651739140054-6b8c4aa2-9d68-4294-952b-7c6e54aac808.png#clientId=u8eedb41c-2f02-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=770&id=ud6acb20d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=963&originWidth=1144&originalType=binary&ratio=1&rotation=0&showTitle=false&size=300193&status=done&style=none&taskId=ub90a22c1-fad3-462a-98ee-629f2ff7b5b&title=&width=915.2)
