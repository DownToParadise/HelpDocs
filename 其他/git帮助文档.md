# Git帮助文档

* ## 1，首次建仓
  
  *首次建仓需要通过git bash 文件夹建仓，首次建仓后就可以通过vscode，pycharm等进行仓库管理*

![avater](https://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg "作区，暂存区，版本区区别")

### 本地建仓

```git
git init        //在想要建仓的文件夹，git bash使用该命令，建立本地仓
                //其他的操作一致
git add XX         //将文件加入暂存区中(前提，将你要上传的文件放入刚刚创建的仓库文件夹中)，                     （将哪些文件要上传，"."表示文件夹全部文件）
                //将该文件记入 Git 仓库的版本管理对象中，计加入暂存区Stage或Index中
git commit         //-m "XXX"    通过-m后的信息进行版本比对后，将最新版本上传至版本区，XXX用于版                    本恢复等，必须与add搭配            
                //--amend  修改当前提交的提交信息
                //--am "XX"实现add和commit的功能，只能对跟踪了的文件进行提交（使用过一次                    add命令），提交信息为XX
git push        //将版本区文件传入github中，将当前HEAD推到远端
git status        //查看当前HEAD状态
git log            //查看当前提交记录，
                //--graph以图表形式查看日志，只能以当前状态为终点的历史日志，通过日志可以                查看对应版本的哈希值用以回溯，该哈希值是该操作产生之后产生的
git reflog        //查看当前仓库的操作日志
git diff        //比较工作区（树），暂存区，最新提交之间的区别，优先比较工作区与暂存区的区                    别，因为一般来说，暂存区的都要提交，
                //git diff HEAD查看工作区与最新提交的差别
git branch XXX    //再当前HEAD上创建一个分支XXX
                //-m A B，将A分支的名称改为B名字
                //-a，查看当前分支的相关信息
                //-f master HEAD~3，强制将master分支名指向HEAD~3
git checkout XXX //将HEAD切换到XXX分支上，
                //使用-b XXX可以创建加切换
                //使用 -b A origin/A 将远程端的A拉取到本地A branch上，并让HEAD对准A
                // - 切换到上一个分支
git merge XXX     //把XX分支合并到当前分支上
git reset         //变基，回溯历史版本，
                //--hard 哈希/HEAD，不产生新的提交， 哈希值根据哈希值将HEAD回溯到历史版                    本，可以在历史版本上再建立分支，称为“推进历史”，甚至可以回溯到相关的操作时                    期
git revert A    //产生一个新的提交，但这个提交是会保留除A以外的所有提交
                //git revert HEAD^去除父提交（可以用于撤销）
git rebase         //更改历史，相当于合并几个提交
                //-i HEAD~n，将HEAD往上几个进入UI界面操作，可以修改提交顺序，也可以将提交                合并成一个。
                //pick为保留提交（改变pick顺序相当于改变提交顺序），fixup为被融合项
git remote add A URL //将远程仓库URL作为一个独立的（remote）branch加入本地仓库，branch名为A
git push -u A B    //将本地仓库推到远程，
                //一般用git push -u origin master，将origin作为master的上游（upstream），                这样在进行git pull更新本地仓库时比较方便，推送其他本地分支同理
git pull        //拉取当前的关联的远程仓库
                //git pull origin A将远程端的A branch的最新状态拉到本地的同名A上（本地A通过                 git checkout -b A origin/A 创建），将HEAD指到本地A上，在用git push 可以                    将本地更新到远程端的A上
git fetch        //大部分功能与git pull一致，但推荐使用git pull(old)        
git cherry-pick <A,B,C ...>//产生新提交，强制将<A,B,C,...>的内容复制到新提交中
                 //git cherry-pick c1 c2 c3，将c1, c2, c3合并作为一个新提交（不消除c1, c2,                     c3）
git tag v1 <结点>//对结点打上v1标签，默认对HEAD结点打标签
```

#### git本地文件推送到远端

* 简单流程
  [参考文档](https://blog.csdn.net/qq_42072311/article/details/80696886)
  **1**，建立git init 建立本地仓库（或者从远端拉取到本地，或解压文件包）
  **2**，在本地仓库，新加或更改文件产生差异。
  **3**，git add将文件添加到本次提交（查询git add -h，git add .添加所有修改文件）
  **4**，git commit -m "xxx"将本次提交加入到本地仓库中，记得加入-m提交评论。
  **5**，git push 将本地仓库推导远端

* 复杂流程
  git rebase，git merge等操作将分支进行合并等操作

### 拉取GitHub仓库进行建仓

*一般在远程仓库中orgin/main为主分支，远程仓库中master为本地上传的分支，*
*也可以将远程仓库直接拉取到本地进行管理*

### 注意：

* ### 在本地建仓后拉取远程仓库的管理与直接拉取远程仓库略有不同*

```git
git clone URL    //在本地中引入URL仓库副本
git pull        //
git fetech        //
```

### 注意事项

* 工作区，暂存区（staged/Index），历史版本区（history）
* 本地（工作区）中的文件显示的内容是根据当前HEAD所指向的提交而定
* 文件对象分为tracked/untracked、staged/staged（放入暂存区），要先track（git add），才能放入暂存区中
* HEAD表示当前提交，HEAD^表示父提交（HEAD^2表示另一个父提交）HEAD^^表示父父提交。
* ~num表示向上移动num个提交，~（不加num） 只移动一个提交。(^和~可用于哈希值出现的地方)
* git体系中分为master（本地仓库）和origin（远程仓库），（本地仓库一般挂在拉取的远程仓库下），仓库有主分支，主分支一般为稳定的版本，分支（branch）一般为增加的功能或者修改版本，分支由多个提交/结点（commit）构成，当前提交由HEAD指定。
* tag标记，tag标记是对当前commit的描述，是只能固定在该提交上，不能像HEAD一样移动，所以标签不能更新。可以通过标签名引用该提交

```shell
shift + zz  //先按exc，再按shift+Z退出vim编辑器模式
```

* ## 2，通过IDE进行二次操作
  
  *通过IDE自带的与GitHub直连的区域进行连接，代开有仓库的文件夹就能在IDE进行Git操作*

* ## 3，各种git问题解决

* OpenSSL SSL_read: Connection was reset, errno 10054 错误解决
  
  https://www.cnblogs.com/zhanqing/p/15133067.html
  
  ```git
  git config --global http.sslVerify "false"
  git config --global https.sslVerify "false"
  ```

* Failed to connect to github.com port 443 after 21064 ms: Timed out
  
  ```git
  该问题由网络原因引起，建议重试，或重新打开，或者使用gitee（码云）
  ```