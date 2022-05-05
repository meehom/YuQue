---

粘包现象
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650954423441-3122bb69-9c2c-48a7-bd6f-848af20a4913.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=702&id=u467948c7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=878&originWidth=1556&originalType=binary&ratio=1&rotation=0&showTitle=false&size=752876&status=done&style=none&taskId=u2d9bfa9a-f3eb-4b37-922e-da0b5a69bc0&title=&width=1244.8)
半包现象
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650954511725-b089c495-8673-4e9d-8f47-521f24bbac75.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=249&id=u7924d5e2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=311&originWidth=987&originalType=binary&ratio=1&rotation=0&showTitle=false&size=341208&status=done&style=none&taskId=u1b48b281-012d-4b98-94e2-0541c2f23cd&title=&width=789.6)


Tcp协议的滑动窗口
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650954576604-592fba57-787e-4517-b3f5-b14e50c3226a.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=391&id=u56847c52&margin=%5Bobject%20Object%5D&name=image.png&originHeight=489&originWidth=582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=179163&status=done&style=none&taskId=u3636bff0-e776-4139-beeb-1fec64be4ae&title=&width=465.6)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650954639233-1da595c3-95e8-4cc6-8581-cc13b3ce6d4e.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=253&id=u46ed1051&margin=%5Bobject%20Object%5D&name=image.png&originHeight=316&originWidth=1168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=209770&status=done&style=none&taskId=ude6e34ce-3ddb-4583-a402-d7319a18dab&title=&width=934.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650954684998-129456c7-bf3e-46cc-854a-2101905b1ec2.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=272&id=uddef0154&margin=%5Bobject%20Object%5D&name=image.png&originHeight=340&originWidth=1122&originalType=binary&ratio=1&rotation=0&showTitle=false&size=228382&status=done&style=none&taskId=ub75f4060-64e9-4af6-ada6-7b5c7a9a864&title=&width=897.6)

## 粘包半包

---

### 短连接

---

- client

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650955112637-4a7d490b-8256-41bb-9065-182eb6d75ffb.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=642&id=ufb0c697c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=802&originWidth=1562&originalType=binary&ratio=1&rotation=0&showTitle=false&size=792689&status=done&style=none&taskId=ud311e65e-e4ae-49b1-8ec1-1465237d24e&title=&width=1249.6)
效率低，解决了粘包，解决不了半包

### 定长发送接收

---

- client

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650955373152-924d3462-c6db-4923-a805-4bf9db843038.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=675&id=ua2444ff7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=844&originWidth=1175&originalType=binary&ratio=1&rotation=0&showTitle=false&size=487282&status=done&style=none&taskId=ufd1aa834-40bc-4185-918a-341770129fb&title=&width=940)

- server

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650955402043-c3d59c6d-1aa5-41fc-acc3-c9a16fde27e0.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=360&id=ud98200f5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=450&originWidth=1173&originalType=binary&ratio=1&rotation=0&showTitle=false&size=394545&status=done&style=none&taskId=u26759013-068f-4c19-b3a4-4af62dc1694&title=&width=938.4)
浪费资源，但是解决了问题


### 分隔符实现

---

- client

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650956376006-b6c7e6d5-f9b4-47af-a587-e75144674017.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=203&id=u4cb580ab&margin=%5Bobject%20Object%5D&name=image.png&originHeight=254&originWidth=825&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127966&status=done&style=none&taskId=ue2180b06-67ea-443c-8205-d0e7cca33c2&title=&width=660)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650956441959-888e0188-2b39-424f-882f-1d1017b6d175.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=494&id=uf7ea731d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=617&originWidth=1096&originalType=binary&ratio=1&rotation=0&showTitle=false&size=422924&status=done&style=none&taskId=u0ec4ca63-235c-46a4-b899-befc44d5de1&title=&width=876.8)

- server

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650956475584-f09d1855-dbce-4ba2-9001-4c13469ad901.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=607&id=u218448a5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=759&originWidth=1109&originalType=binary&ratio=1&rotation=0&showTitle=false&size=639295&status=done&style=none&taskId=udd46d6e2-81b4-49da-9a32-3d6a0ed6cf4&title=&width=887.2)

### LTC实现

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650956574209-1165f722-11ff-4eb4-8efc-b434c96e37bf.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=110&id=u56c6a8f1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=137&originWidth=727&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99015&status=done&style=none&taskId=u01987758-51e8-4a7b-8557-d96e3535b56&title=&width=581.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650956858181-ea86dc1a-0922-4fde-9fca-ac4eeed52c5d.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=626&id=u04e2ec36&margin=%5Bobject%20Object%5D&name=image.png&originHeight=783&originWidth=1679&originalType=binary&ratio=1&rotation=0&showTitle=false&size=580648&status=done&style=none&taskId=u2af0e6b0-6024-44ba-b626-79cc41af2e9&title=&width=1343.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650956948669-58435716-fbe2-48a9-a3ce-80c5e42e61b8.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=320&id=u03c7dade&margin=%5Bobject%20Object%5D&name=image.png&originHeight=400&originWidth=1208&originalType=binary&ratio=1&rotation=0&showTitle=false&size=329436&status=done&style=none&taskId=ubaa6b4ab-37a8-4b78-a756-6154b560b38&title=&width=966.4)

- 加入版本

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650957013236-d20e0787-6d8e-45dd-b4a0-ee31b66ffa1b.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=675&id=u22c382f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=844&originWidth=1679&originalType=binary&ratio=1&rotation=0&showTitle=false&size=621031&status=done&style=none&taskId=u5267fdd8-3aa0-40ea-a771-0ef2b984200&title=&width=1343.2)



## 协议解析与设计

---

### redis解析

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650957307737-9776e22f-65be-40ea-ab67-f4304f8c2c84.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=558&id=ua00ba38b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=698&originWidth=1103&originalType=binary&ratio=1&rotation=0&showTitle=false&size=575861&status=done&style=none&taskId=uf6bc8d3c-0217-465a-8e55-43c0f3aef47&title=&width=882.4)


### Http解析

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650957639097-1893e74f-c647-4dba-aa79-46966d450043.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=706&id=uee9f1765&margin=%5Bobject%20Object%5D&name=image.png&originHeight=882&originWidth=1415&originalType=binary&ratio=1&rotation=0&showTitle=false&size=733190&status=done&style=none&taskId=ud7090ab9-8059-437c-a59e-1940c765f08&title=&width=1132)


### 自定义协议

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650957969353-57d50e39-6213-4dd6-982e-25e62ef31ef7.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=338&id=ud59e4c5a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=423&originWidth=1051&originalType=binary&ratio=1&rotation=0&showTitle=false&size=301001&status=done&style=none&taskId=u62b8c65c-8891-4052-a3fd-e87df17ddd3&title=&width=840.8)

- 编码

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650958263141-ba0b22ae-ad7b-4076-a1b1-76e9f1608212.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=698&id=u250b4e8d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=872&originWidth=1095&originalType=binary&ratio=1&rotation=0&showTitle=false&size=608291&status=done&style=none&taskId=uc02bd811-72df-4ff3-ae65-4a78c05c4c0&title=&width=876)

- 解码

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650958319636-0d630ae2-b267-4081-b2c2-2285fc5803c4.png#clientId=u21133a79-735b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=490&id=u4defc4e3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=612&originWidth=1490&originalType=binary&ratio=1&rotation=0&showTitle=false&size=512445&status=done&style=none&taskId=u1fd9046e-f207-4b0e-88f7-9d759fb0cf9&title=&width=1192)


## 聊天室

---


