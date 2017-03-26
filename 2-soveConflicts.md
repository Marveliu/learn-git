How to solve conflicts
=====

> 如果一个project出现了conflicts,除了自身的项目构建问题之外，还有就是要解决当前面临的问题，合并
所谓，冲突就是分支之前出现了分叉
>
> 假设两个分支: origin,mywork


origin是云端的分支，mywork是本地的分支，当你add->commit->push,git console提示rejected,这意味着你需要git pull,即云端和你本地的文件不一致，
有交叉修改的部分,然后使用git pull,出现了问题

# git rebase

> rebase 重定基底
        
        $ git checkout mywork
        $ git rebase origin

这些命令会把你的"mywork"分支里的每个提交(commit)取消掉，并且把它们临时 保存为补丁(patch)(这些补丁放到".git/rebase"目录中),然后把"mywork"分支更新 到最新的"origin"分支，最后把保存的这些补丁应用到"mywork"分支上。

当'mywork'分支更新之后，它会指向这些新创建的提交(commit),而那些老的提交会被丢弃。 如果运行垃圾收集命令(pruning garbage collection), 这些被丢弃的提交就会删除.

在rebase的过程中，也许会出现冲突(conflict). 在这种情况，Git会停止rebase并会让你去解决 冲突；在解决完冲突后，用"git-add"命令去更新这些内容的索引(index), 然后，你无需执行 git-commit,只要执行

        $ git rebase --continue
    
在任何时候，你可以用--abort参数来终止rebase的行动，并且"mywork" 分支会回到rebase开始前的状态。

        $ git rebase --abort

> 最后无脑修改
>       
>       $ git rebase --abort