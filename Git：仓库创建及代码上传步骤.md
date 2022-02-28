## 新建仓库：

Your repositories -> New -> Create repository

## git上传：

**本地Git仓库：**

- 新建文件夹作为本地的版本库

- `git init`  初始化仓库
- `git add .`
- `git commit -m '注释内容'`

**远程Git仓库：**

- 配置用户信息

  - `git config --global user.name "yourName"`

  - `git config --global user.email "yourEmail@example.com"`

    <!--查看用户名：git config user.name-->

    <!--查看邮箱地址：git config user.email-->

- 创建SSH KEY  

  - `ssh-keygen`

    <!--查看是否已生成ssh密钥：`cd ~/.ssh/`-->

- 配置SSH KEY

  - `C:\Users\xxx\.ssh` 目录下，复制`id_rsa.pub`内容
  - `Settings` ->  `SSH and GPG keys` -> `new SSH key`

**关联远程仓库：**

- `git remote add origin https://github.com/xxxx/xxx.git`

**将本地分支内容推送到远程分支：**

- `git push -u origin master`

<!--由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需执行 git push origin master-->

## github生成person access token：

1. 登录 github,点击右上角选择setting
2. 左侧列表选择Developer settings
3. 选择Prsonal access token, 点击generate new token
4. 起个名，权限选择全部就行
5. 最下面选择 generate token
6. 把token复制出来，不要忘记，只会显示一次



## git push 出现`fatal: unable to access 'https://github`

`git push -u origin master`时报错

<!--fatal: unable to access 'https://github.com/....git/': Failed to connect to github.com port 443: Timed out-->

- 有可能gitbub之前设置过代理
  - 查询http代理：`git config --global http.proxy` 
  - 查询https代理：`git config --global https.proxy` 
- 取消代理：
  - `git config --global --unset https.proxy`

- 如果还没有解决，可以尝试如下解决方式，亲测有效：
  - `git config --global url.git://github.com/.insteadOf https://github.com/`
