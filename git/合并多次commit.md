1. git log 查看提交记录
2. git rebase -i HEAD~3 进入合并操作的vim界面 

  HEAD~3表示将最近三次commit的修改合并到第一次的commit中
>pick：保留该commit（缩写:p）

>reword：保留该commit，但我需要修改该commit的注释（缩写:r）

>edit：保留该commit, 但我要停下来修改该提交(不仅仅修改注释)（缩写:e）

>squash：将该commit和前一个commit合并（缩写:s）

>fixup：将该commit和前一个commit合并，但我不要保留该提交的注释信息（缩写:f）

>exec：执行shell命令（缩写:x）

>drop：我要丢弃该commit（缩写:d）
