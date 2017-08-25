# Hexo博客源文件备份
首先我们假设你已经会使用Hexo搭建自己的博客了
如果有不清楚的同学，请移步[官方网站](https://hexo.io/)先安装hexo，并学会使用至少
```
hexo s
hexo g
hexo d
```
这三个命令~
## 实现方法:

* 在Github下创建一个新的repository，取名为myBlog。
* 在本地创建一个blog文件夹，将你的博客源文件Hexo文件夹放在blog里面。
* 进入本地的blog文件夹，执行以下命令创建仓库:
```
git init
```

* 设置远程仓库地址，并更新:
```
git remote add origin https://github.com/yourname/myBlog.git 
git pull origin master
```
* 修改.gitignore文件（如果没有请手动创建一个），在里面加入*.log 和 public/ 以及.deploy*/。因为每次执行hexo generate命令时，上述目录都会被重写更新。因此忽略这两个目录下的文件更新，加快push速度。
* 执行命令以下命令，完成Hexo源码在本地的提交。
```
git add .
git commit -m "init hexo backup"
```
* 执行以下命令，将本地的仓库文件推送到Github。
```
git push origin master
```

* 现在在任何一台电脑上，只需要执行
```
git clone https://github.com/yourname/myBlog.git 
```
即可完成将Hexo源文件复制到本地（请将`yourname/myBlog.git`替换为自己相应的仓库地址。）

* 在本地编写完博客时，顺次执行以下命令，即可完成Hexo博客源文件的更新同步，保持Github上的hexo源码为最新版本。
```
git add .
git commit -m "update"
git push origin master
```
* 当远程仓库有更新时，执行以下命令，即可同步hexo源文件到本地。

```
git pull origin master
```
至此，Hexo源代码文件就完成了同步和更新了。

* 如果要预览本地的博客，只需要在本地执行
```
cd ./blog/HEXO
hexo g
hexo s
```
之后在浏览器里输入 http://127.0.0.1:4000/ 就可以看到自己的博客了。
