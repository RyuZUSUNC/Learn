# github

- Repository name: 仓库名称

- Description(可选): 仓库描述介绍

- Public, Private : 仓库权限（公开共享，私有或指定合作者）

- nitialize this repository with a README: 添加一个README.md

- gitignore: 不需要进行版本管理的仓库类型，对应生成文件.gitignore

- license: 证书类型，对应生成文件LICENSE

# git命令
- git clone `[URL]` ¿ 把github上面的仓库克隆到本地

- git init ¿ 把当前文件夹变成Git可管理的仓库

- git add . ¿ 把Test文件夹下面的文件都添加进来

- git commit  -m  "[ user message ]" ¿ 将文件置入上传仓库

- git push -u origin master ¿ 把本地仓库push到github上面

---
- git help `<command>` ¿ 显示command的help  

- git show ¿ 显示某次提交的内容 git show $id  

- git co -- `<file>` ¿ 抛弃工作区修改  

- git co . ¿ 抛弃工作区修改  

- git add `<file>` ¿ 将工作文件修改提交到本地暂存区  

- git add . ¿ 将所有修改过的工作文件提交暂存区  

- git rm `<file>` ¿ 从版本库中删除文件  

- git rm `<file>` --cached ¿ 从版本库中删除文件，但不删除文件  

- git reset `<file>` ¿ 从暂存区恢复到工作文件  

- git reset -- . ¿ 从暂存区恢复到工作文件  

- git reset --hard ¿ 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改  

- git ci `<file>` git ci . git ci -a ¿ 将git add, git rm和git ci等操作都合并在一起做　　　　　　　　　　
　　　　　　　　　　　　　　　　　　　　　　　　　
- git ci -am "some comments"  

- git ci --amend ¿ 修改最后一次提交记录  

- git revert <$id> ¿ 恢复某次提交的状态，恢复动作本身也创建次提交对象  

- git revert HEAD ¿ 恢复最后一次提交的状态  
---
## 查看提交记录

- git log git log `<file>` ¿ 查看该文件每次提交记录  

- git log -p `<file>` ¿ 查看每次详细修改内容的diff  

- git log -p -2 ¿ 查看最近两次详细修改内容的diff  

- git log --stat ¿ 查看提交统计信息  
---
## Git 本地分支管理

git br -r ¿ 查看远程分支  

git br `<new_branch>` ¿ 创建新的分支  

git br -v ¿ 查看各个分支最后提交信息  

git br --merged ¿ 查看已经被合并到当前分支的分支  

git br --no-merged ¿ 查看尚未被合并到当前分支的分支  

git co `<branch>` ¿ 切换到某个分支  

git co -b `<new_branch>` ¿ 创建新的分支，并且切换过去  

git co -b `<new_branch>` `<branch>` ¿ 基于branch创建新的new_branch  

git co $id ¿ 把某次历史提交记录checkout出来，但无分支信息，切换到其他分支会自动删除  

git co $id -b `<new_branch>` ¿ 把某次历史提交记录checkout出来，创建成一个分支  

git br -d `<branch>` ¿ 删除某个分支  

git br -D `<branch>` ¿ 强制删除某个分支 (未被合并的分支被删除的时候需要强制)  

