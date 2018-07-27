title: Hexo博客(二)主题&图床&管理
author: liuleihang
date: 2018-07-27 23:45:16
tags:
---
## 更换主题

### Next主题
- 下载主题
    ```
    $ git clone https://github.com/iissnan/hexo-theme-next themes/next
    ```
    ```
    Cloning into 'themes/next'...
    remote: Counting objects: 12025, done.
    remote: Compressing objects: 100% (4/4), done.
    remote: Total 12025 (delta 1), reused 1 (delta 1), pack-reused 12020
    Receiving objects: 100% (12025/12025), 12.99 MiB | 894.00 KiB/s, done.
    Resolving deltas: 100% (7008/7008), done.
    Checking out files: 100% (351/351), done.

    ```
- 修改主_config.yml配置文件
    ```
    # Extensions
    ## Plugins: https://hexo.io/plugins/
    ## Themes: https://hexo.io/themes/
    #theme: landscape
    theme: next
    ```
## 使用七牛云存储图床
### 到https://www.qiniu.com注册七牛帐号,实名认证会开启更多功能
### 新建对象存储空间blog-hexo-corner
    
    图1

### 上传图片及使用
- 内容管理-
- 命令行上传工具
    https://developer.qiniu.com/kodo/tools/1302/qshell
- 使用图片

    粘贴到你想使用的地方，当然也可以使用浏览器直接打开，主要是在hexo中使用，在Markdown中采用
    ```
    ![image](你的外链地址)
    ```

## Hexo后台管理
http://www.cnblogs.com/xingyunblog/p/8681205.html