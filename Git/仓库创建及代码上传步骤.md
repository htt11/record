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

## git push origin dev 时报错：

**报错信息：**<!--error: failed to push some refs to 'git.staff.sina.com.cn:nevis.io/ui/nevis_admin.git'-->

原因：github中的README.md文件不在本地代码目录中

解决：进行代码合并【注：pull=fetch+merge]

```git
git pull --rebase origin 
```

执行后：本地代码库中多了README.md文件

再执行语句 git push -u origin master即可完成代码上传到github

<!--$ git push origin master 报错-->

```git
error: failed to push some refs to 'git.staff.sina.com.cn:nevis.io/ui/nevis_idb.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

解决：

```git
git pull --rebase origin master
git push origin master
```

**报错信息：**<!--fatal: unable to access ‘https://github.com/.......‘: OpenSSL SSL_read: Connection was reset-->

- 原因：一般是这是因为服务器的SSL证书没有经过第三方机构的签署，所以才报错
- 解决：
  - 解除ssl验证： `git config --global http.sslVerify "false"`   
  - 重新push



## 补充：

### 查看用户名和邮箱地址：

```
git config user.name 
git config user.email 
```

### 修改用户名和邮箱地址： 

```
git config --global user.name "username"  
git config --global user.email "email"
```

<!--报错：cannot overwrite multiple values with a single value Use a regexp, --add or --replace-all-->

```
原因：有可能是名字重复了，如果要替换则按下面执行
解决：git config --global --replace-all user.name "输入你的用户名"
查看效果：git config --list 
```

<!--报错：-->

<!--fatal: You have not concluded your merge (MERGE_HEAD exists).-->
<!--Please, commit your changes before you merge.-->

```
原因：没有拉取代码。
解决办法:保留本地的更改,中止合并->重新合并->重新拉取
	git merge --abort   //中止合并
	git reset --merge   //撤销合并
	git pull            //拉去代码
```

### 取消commit：

```
git log    -- 查看记录
git reset --soft HEAD^    --取消commit
git reset --hard HEAD^    --连着也取消add
git status    --查看状态
```

<!--撤回上一次：HEAD^ / HEAD~1-->

<!--撤回前两次：HEAD^^ / HEAD~2-->
