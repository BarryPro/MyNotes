## GitHub-笔记仓库

### 一、把笔记提到GitHub的步骤

1. 在GitHub上创建项目
2. 使用 git clone https://github.com//.git   // git上的地址
3. 编辑项目
4. git add .  // 将改动添加到暂存区
5. git commit -m “提交说明”
6. git push origin master  // 将本地更改推送到远程master分支

### 二、如果GitHub的remote上已经有文件了，会出现错误，解决方式

``` git
git pull origin master
```

``` git
git push origin master
```



