==**yy-复制**==、==**p-粘贴**==
==**i-进入插入模式**==、==**Esc-进入命令模式**==
==**命令模式中，按“shift”+”；“，在输入wq，进行保存**==

| 命令名称                              | 作用      |
| --------------------------------- | ------- |
| git config --global user.name 用户名 | 设置用户签名  |
| git config --global user.email 邮箱 | 设置用户签名  |
| git init                          | 初始化本地库  |
| git status                        | 查看本地库状态 |
| git add 文件名                       | 添加到暂存区  |
| git commit -m"日志信息"文件名            | 提交到本地库  |
| git reflog                        | 查看历史纪录  |
| git reset --hard 版本号              | 版本穿梭    |
### 初始化本地库
git init
- 点进文件夹，鼠标点击右键，选择“Open Git Bash Here”,输入“ll -a”可查看文件路径

### 查看本地库状态
git status
- 输入“git status”可查看三行日志
“On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)”
- 第一行：表示这个本地库在master这个分支里
- 第二行：表示当前还没提交任何东西
- 第三行：还没什么东西可以提交

创建文本：输入”vim hello.txt“
==**yy-复制**==、==**p-粘贴**==
==**i-进入插入模式**==、==**Esc-进入命令模式**==
==**命令模式中，按“shift”+”；“，在输入wq，进行保存**==
cat+"文件名"可查看文件内容
tail -n 1+“文件名”可查看文件末尾最后一行

### 添加到暂存区
git add 文件名
暂存区中删除文件："git rm --cached 文件名"

### 提交到本地库 & 查看历史纪录
git commit -m"日志信息"文件名  提交到本地库
git reflog                                     查看历史纪录
git log                                         查看详细日志

### 修改文件
输入"vim hello.txt"

### 版本穿梭
git reset --hard 版本号