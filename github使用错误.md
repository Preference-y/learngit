# Git使用常见错误

## error:failed to push some refs to 'xxx'

本地仓库没有Readme文件，先PULL下远程仓库
`git pull --rebase origin master`
`git push -u origin master`
PS:pull=fetch+merge

------

## error: GH007: Your push would publish a private email address.

由于设置了邮箱为隐私邮箱，有两种解决方式：

1. 在GITHUB上setting-Emails-Keep my email addredd private去掉勾选。
2. 或者命令行中配置邮箱为username@users.noreply.github.com
   `git config --global user.email 'username@users.noreply.github.com'`

------

## fatal:remote origin already exists

1. 删除远程GIT仓库链接
   `git remote rm origin`
2. 重新添加GIT仓库
   `git remote add origin git@github.com:用户名/项目名.git`





## GitHub报错：error: GH007: Your push would publish a private email address.





在GitHub的隐私设置中勾选了`Block command line pushes that expose my email`后，再次提交的Git项目中如果提交暴露私人邮箱地址的commit时会报错



```
remote: error: GH007: Your push would publish a private email address.
remote: You can make your email public or disable this protection by visiting:
remote: http://github.com/settings/emails
To github.com:xxxx/xxxx.git
 ! [remote rejected] master -> master (push declined due to email privacy restrictions)
error: failed to push some refs to 'git@github.com:xxxx/xxxx.git'
```



网上搜索了一下，大多提供的解决方案都是取消`Keep my email address private`，这显然违背了GitHub提供这个功能的初衷，并且会公开你的私人邮箱
真正的解决方案应该是修改Git中的邮箱地址为GitHub提供的匿名邮箱才对

```
# 修改全局邮件地址
git config --global user.email "用户名@users.noreply.github.com"
git config user.email "用户名@users.noreply.github.com"
# 重置 commit 的作者信息
git commit --amend --reset-author
# 再次提交
git push
```

