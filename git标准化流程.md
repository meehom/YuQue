---

1.项目代码（刚开始是一个空的仓库）
一般有3个分支

- master（线上分支）
- dev（开发分支）
- test（测试分支）

2.fork到本地分支
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651064728685-c31d9b2d-47f8-4aa3-9dd0-e8c47a9de4f2.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=91&id=ub7d0af15&margin=%5Bobject%20Object%5D&name=image.png&originHeight=91&originWidth=540&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9417&status=done&style=none&taskId=u49a7da91-30df-42f8-b544-83dfa7544bf&title=&width=540)

3.clone到本地
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651064794681-0e5f9045-6a0b-4c9c-b51f-981eb4072c79.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=79&id=u8d73c981&margin=%5Bobject%20Object%5D&name=image.png&originHeight=79&originWidth=501&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8307&status=done&style=none&taskId=u9705372f-fd33-4cf6-9029-1840f878829&title=&width=501)

4.修改远程仓库名
> 一般远程仓库为项目代码，origin仓库为自己fork的仓库

```bash
git remote add upstream https://github.com/Lavender-QAQ/My-Acwing-Code
```


5.在分支上开发自己的功能
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651065046876-b6864f66-e12e-4168-a63e-24858cf8d069.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=125&id=u589edb99&margin=%5Bobject%20Object%5D&name=image.png&originHeight=125&originWidth=737&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13429&status=done&style=none&taskId=u7ebcf06d-e97f-4d33-844c-4459b3ff8ac&title=&width=737)

6.完成功能后push上去
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651065133354-7a370067-393d-4832-8823-8e66aaff49b8.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=104&id=uf6092a7c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=104&originWidth=743&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8332&status=done&style=none&taskId=u672e040a-389f-4d6a-888a-d7d6ce2f3e1&title=&width=743)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651065171999-b0155105-2bb7-4b2f-92ff-8a853d8bd18e.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=80&id=udbf173a0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=80&originWidth=722&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7617&status=done&style=none&taskId=u7b710b8f-a43d-40ee-a726-aef9d618f42&title=&width=722)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651066976234-718b5ca0-f8a2-4f8a-8954-f8cb3a1dd180.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=268&id=u3ad883c0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=268&originWidth=786&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36010&status=done&style=none&taskId=ud3c17dd3-9321-4c35-95a2-fc2bef45911&title=&width=786)

7.在github上提交一个pull request
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1651067057339-d4a85e2a-24bc-4f01-a2dc-2862b6cf857e.png#clientId=u5e30173c-8734-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=895&id=u404fc13e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=895&originWidth=1371&originalType=binary&ratio=1&rotation=0&showTitle=false&size=90374&status=done&style=none&taskId=u5f892fc4-04a7-4c89-92f3-35717421705&title=&width=1371)

等待对方审核过后，一个需求就完成了

其他命令
git remote 查看所有的远程分支
一般有origin 和 upstream

git diff readme.txt 查看readme.txt做了哪些修改

git log 查看历史版本， git log --pretty=oneline 简洁输出

git reset --hard Head^ 回退到上一个版本 Head^^ 上两个版本 Head~10前10个版本

git reflog 记录每一行命令，可以让你回退版本后还能回去

git checkout -- reader.txt 让文件回到最近一次git commit 或 git add 的状态（目前好像为git restore了）

git reset HEAD readme.txt 也可以把暂存区的修改回退

git rm readme.txt 删除文件

git stash 储存工作现场，可以在你开发一个功能到一半，又来了一个紧急需求的时候

git stash pop 恢复现场

git branch -D feature-vul 强制删除某个分支

git tag v1.0 打一个标签






