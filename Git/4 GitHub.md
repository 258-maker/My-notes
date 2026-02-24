HTTPS-远程库

| 命令名称                   | 作用                           |
| ---------------------- | ---------------------------- |
| git remote -v          | 查看当前所有远程地址别名                 |
| git remote add 别名 远程地址 | 起别名                          |
| git push 别名 分支         | 推送本地分支上的内容到远程仓库              |
| git clone 远程地址         | 将远程仓库的内容复制到本地                |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |
### 创建别名
git remote add 别名 远程地址            起别名

Git-Demo        https://github.com/258-maker/Git-Demo.git (fetch)拉取
Git-Demo        https://github.com/258-maker/Git-Demo.git (push)推送


clone会做如下操作：1、拉取代码；2、初始化本地仓库；3、创建别名

### 删除分支
- 删除远程分支：git push 远程仓库名 --delete
