title: Hexo博客(一)创建
tags:
  - Hexo
categories: []
date: 2018-04-19 16:43:00
---
## 准备

### 已经安装Git和配置好Git环境

### 已经注册Github帐号

### Github上新建项目

​	登录Github新建项目，项目必须要遵守格式：账户名.github.io，不然接下来会有很多麻烦。并且需要勾选Initialize this repository with a README

![新建项目](http://p6uif5qvi.bkt.clouddn.com/images/3-1-createRepository.png)

## 安装node版本管理工具NVM

### 安装NVM

- NVM Github地址

  ```
  https://github.com/coreybutler/nvm-windows
  ```


- 电脑上安装，选择合适的安装路径一路下一步。

- NVM常用命令

  ```
   nvm list        /*列出node.js列表*/
   nvm on          /*启用node.js版本管理*/
   nvm off         /*禁用node.js版本管理（不会卸载任何东西）*/
   nvm use <version>     /*切换到使用指定的版本*/
   nvm version           /*显示当前正在运行的NVM for Windows版本*/
   nvm install <version> /*安装指定版本的nodejs*/
   nvm uninstall <version> /*卸载指定版本*/
   nvm node_mirror <node_mirror_url> /*设置node下载镜像*/
   nvm npm_mirror <node_mirror_url> /*设置npm下载镜像*/
  ```



## 安装nodejs和配置npm

### 使用nvm安装nodejs

- 安装nodejs@8.11.1

  ```
  C:\WINDOWS\system32>nvm install 8.11.1
  Downloading node.js version 8.11.1 (64-bit)...
  Complete
  Creating d:\nvm\temp

  Downloading npm version 5.6.0... Complete
  Installing npm v5.6.0...

  Installation complete. If you want to use this version, type

  nvm use 8.11.1
  ```

- 使用对应版本的nodejs

  ```
  nvm use 8.11.1
  ```

- npm配置

  ```
  npm config set cache "D:\nodejs\node_tmp"
  npm config set userconfig"D:\nodejs\etc\.npmrc"
  npm config set registry https://registry.npm.taobao.org
  ```




## 安装和配置Hexo

### 安装hexo

- npm install hexo -g

- hexo -v，检查hexo是否安装成功

  ```
  C:\WINDOWS\system32>hexo version
  hexo-cli: 1.1.0
  os: Windows_NT 10.0.16299 win32 x64
  http_parser: 2.8.0
  node: 8.11.1
  v8: 6.2.414.50
  uv: 1.19.1
  zlib: 1.2.11
  ares: 1.10.1-DEV
  modules: 57
  nghttp2: 1.25.0
  openssl: 1.0.2o
  icu: 60.1
  unicode: 10.0
  cldr: 32.0
  tz: 2017c
  ```

### 创建blog工程
- 创建blog文件夹并进入，初始hexo

  ```
  hexo init
  ```


  ![hexo init](http://p6uif5qvi.bkt.clouddn.com/images/3-3-1-hexo-init.png)

- 生成静态文件

  ```
  hexo generate
  ```
  ![hexo g](http://p6uif5qvi.bkt.clouddn.com/images/3-3-2-hexo-g.png)

- 文件结构

  ```
  .
  ├── .deploy #需要部署的文件
  ├── node_modules #Hexo插件
  ├── public #生成的静态网页文件
  ├── scaffolds #模板
  ├── source #博客正文和其他源文件，404、favicon、CNAME 都应该放在这里
  | ├── _drafts #草稿
  | └── _posts #文章
  ├── themes #主题
  ├── _config.yml #全局配置文件
  └── package.json
  ```

- 启动服务器。默认情况下，访问网址为： http://localhost:4000/

  ```
  hexo server
  ```
  ![hexo s](http://p6uif5qvi.bkt.clouddn.com/images/3-3-3-hexo-s.png)

  浏览器地址栏输入127.0.0.1:4000出现一下界面就是启动成功了
  ![hexo启动成功](http://p6uif5qvi.bkt.clouddn.com/image/%28%E4%B8%80%293-2-4-hexo%E5%AE%89%E8%A3%85%E6%88%90%E5%8A%9F.png)

### 将Hexo与Github page联系起来

- 设置Git的user name和email

  ```
  $ git config --global user.name "youname"
  $ git config --global user.email  "youmail"
  ```


- 生成密钥

  - 生成新的 SSH Key：

  ```
  ssh-keygen -t rsa -C "youremail"

  -t 指定要创建的密钥类型。可以使用："rsa1"(SSH-1) "rsa"(SSH-2) "dsa"(SSH-2)
  -C  提供一个新注释
  ```

  ​	在回车中会提示你输入一个密码，这个密码会在你提交项目时使用，如果为空的话提交项目时则不用输入。这个设置是防止别人往你的项目里提交内容。存放目录是c:/Users/hang/.ssh

  ![](http://p6uif5qvi.bkt.clouddn.com/images/3-4-1-ssh-keygen1.png)

  - 添加密钥到ssh-agent

  ```
  eval "$(ssh-agent -s)"
  ```

  添加生成的SSH key到ssh-agent

  ```
  ssh-add ~/.ssh/id_rsa
  ```


- 在Github上添加SSH Keys

  ​	登录Github，点击头像下的settings>>SSH and GPG keys >>New SSH key 新建一个new ssh key，将id_rsa.pub(公钥)文件里的内容全部复制上去

  ![github-SSH-keys](http://p6uif5qvi.bkt.clouddn.com/images/3-4-2-github-SSH-Keys.png)

  ![](http://p6uif5qvi.bkt.clouddn.com/images/3-4-3-github-SSH-Keys.png)

- 测试添加ssh是否成功。中间会提示你是否连接和输入生成ssh key时的密码

  $ ssh -T git@github.com

  ![](http://p6uif5qvi.bkt.clouddn.com/images/3-4-4-ssh-T.png)


- 问题：假如ssh-key配置失败，那么只要以下步骤就能完全解决<br/>

  首先，清除所有的key-pair	

  ```
  ssh-add -D
  rm -r ~/.ssh
  ```

  删除你在github中的public-key,
  重新生成ssh密钥对，重新添加到github上。

  ​


## 创建内容和发布
### 创建文章
- hexo new post "文章名"

  ```
  G:\2.workplace\blog>hexo new post "Hexo博客创建"
  INFO  Created: G:\2.workplace\blog\source\_posts\Hexo博客创建.md
  ```

### 安装一个Hexo插件

- 安装hexo-deployer-git

  ```
  npm install hexo-deployer-git --save
  ```

### 发布项目到github

- 清理下项目缓存

  ```
  hexo clean
  ```


- 配置Deployment

  在其文件夹中，找到_config.yml文件，修改repo值（在末尾）,repo值是你在github项目里的ssh（右下角）Clone or download>>Clone with SSH

  **PS:如果你在生成SSH Keys的时候设置了密码，repository地址需要使用https地址 **

  ```
  deploy:
    type: git
    repository: ssh://your github URL
    branch: master
  ```

- 发布到github上

  ```
  hexo deploy -g   
  -g 部署之前预先生成静态文件
  ```
  ![](http://p6uif5qvi.bkt.clouddn.com/images/4-3-1-hexo-d-g.png)

- 遇到如下问题：

  ```
  Warning: Permanently added the RSA host key for IP address '13.250.177.223' to the list of known hosts.
  git@github.com: Permission denied (publickey).
  fatal: Could not read from remote repository.

  Please make sure you have the correct access rights
  and the repository exists.
  FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
  Error: Warning: Permanently added the RSA host key for IP address '13.250.177.223' to the list of known hosts.
  git@github.com: Permission denied (publickey).
  fatal: Could not read from remote repository.

  Please make sure you have the correct access rights
  and the repository exists.

      at ChildProcess.<anonymous> (G:\2.workplace\blog\node_modules\hexo-util\lib\spawn.js:37:17)
      at emitTwo (events.js:126:13)
      at ChildProcess.emit (events.js:214:7)
      at ChildProcess.cp.emit (G:\2.workplace\blog\node_modules\cross-spawn\lib\enoent.js:40:29)
      at maybeClose (internal/child_process.js:925:16)
      at Process.ChildProcess._handle.onexit (internal/child_process.js:209:5)
  ```

  各种谷歌和百度，解决方案如下：

  将_config.yml中的repository修改为https

  ```
  deploy:
    type: git
    repository: https://your github URL
    branch: master
  ```

  重新执行hexo deploy -g ，最后会有一个弹窗，第一次会让你登录git帐号，显示一下信息，成功！

  ![](http://p6uif5qvi.bkt.clouddn.com/images/4-3-2-hexo-d-g.png)




## 绑定阿里云域名

- 将域名添加到github项目里
    github网站的项目下Setings>>GitHub Page>>Custom domain，填上域名保存即可。

    ![](http://p6uif5qvi.bkt.clouddn.com/images/5-1-1.png)

- [blog.liuleihang.cn](http://blog.liuleihang.cn)

**参考**
- https://www.cnblogs.com/fengxiongZz/p/7707219.html
- https://www.jianshu.com/p/05289a4bc8b2