title: Hexo博客(三)同步更新
author: liuleihang
date: 2018-07-27 23:48:16
tags:
---

名词
```
Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库
```
常用命令
https://www.cnblogs.com/chenwolong/p/GIT.html
```
 git config --list  配置列表
 git status   检查当前文件状态
 git checkout hexo  #切换分支
 git clone <版本库的网址> <本地目录名>   #克隆远程库并指定不同的目录名
 git submodule update --init --recursive  #从远程库下载子模块
 git clone yougiturl --recursive  #采用递归的方式clone整个项目(包含子项目时)
 git add <change file>  #将文件添加到stage
 git commit -m  <message>  #提交修改文件到本地库，标记提交信息
 git push origin branch #将本地库推送到远程库
 git pull 从另一个存储库或本地分支获取并集成(整合)https://blog.csdn.net/qq_15037231/article/details/77937402
 git clean -d -fx表示：删除一些没有git add的文件（慎用，不可恢复）
```

git reflog命令查看你的历史变更记录，
然后可以使用git reset --hard HEAD@{n}，（n是你要回退到的引用位置）回退


需要拷贝的

_config.yml，theme/，source/，scaffolds/，package.json，.gitignore

需要删除

.git/，node_modules/，public/，.deploy_git/，db.json




### 克隆gitHub上面生成的静态文件到本地
```
git clone https://github.com/yourname/hexo-test.github.io.git
```

### github创建并切换到分支hexo
```
git checkout -b hexo
```

### 提交复制过来的文件到暂存区
```
git add --all
```
有时会出现一下错误

```
warning: LF will be replaced by CRLF in hexo/package-lock.json.
The file will have its original line endings in your working directory.
```
这是因为文件中换行符的差别导致的。这个提示的意思是说：会把windows格式（CRLF）转换成Unix格式（LF），这些是转换文件格式的警告，不影响使用。

### 提交源文件

```
 git commit -m ./
```

### 推送分支到github
```
git push --set-upstream origin hexo
```

这样每次写完博客发布之后不要忘了还要git push把hexo源文件push到分支上。



- 这里引出一个知识点，git submodule（子模块）。

  git push成功之后去github网站上验证是否push成功，发现themes/next主题文件夹点不开。[在这里](https://git-scm.com/book/zh/v2/Git-工具-子模块)找到了答案。原因是因为当时next主题也是通过git clone下载的，也是一个独立的版本库。所以最好是当作一个子模块添加到你的库里边。

以后如果要在其他电脑上面用hexo写博客，就可以直接把创建的分支克隆下来，然后npm install安装依赖就可以用了。具体操作如下：

- 克隆分支
```
git clone -b <branchname> "yourgithub" "dirname" --recursive

--recursive  #递归下载子模块
```
- 初始化node_modules,从package.json下载依赖
```
npm install
```

### 删除文件的提交记录（会删除github上的文件，提前备份）
https://help.github.com/articles/removing-sensitive-data-from-a-repository/
https://blog.csdn.net/ysy950803/article/details/53383582

```
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch _config.yml' --prune-empty --tag-name-filter cat -- --all

git push origin hexo --force

rm -rf .git/refs/original/

git reflog expire --expire=now --all

git gc --prune=now

git gc --aggressive --prune=now
```




参考
https://www.jianshu.com/p/beb8d611340a
https://www.zhihu.com/question/21193762
http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/

https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%85%B3%E4%BA%8E%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6