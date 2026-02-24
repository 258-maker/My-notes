

| 命令名称             | 作用             |
| ---------------- | -------------- |
| git branch 分支名   | 创建分支           |
| git branch -v    | 查看分支           |
| git checkout 分支名 | 切换分支           |
| git merge 分支名    | 把指定的分支合并到当前分支上 |

### 查看分支 & 创建分支 & 切换分支 & 修改分支
git branch 分支名           创建分支
git branch -v                  查看分支
git checkout 分支名        切换分支
输入"vim hello.txt"，进行修改

### 合并分支
git merge 分支名              把指定的分支合并到当前分支上
将hot-fix分支合并到master上，要站在master上，使用git merge

### 合并冲突
原因：合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改，Git无法替我们决定使用哪一个，必须人为决定新代码内容。
git commit 时不加文件名