# Git 常用命令总结

## 一、配置命令

### 用户信息配置
```bash
git config --global user.name "用户名"           # 设置用户名
git config --global user.email "邮箱"            # 设置邮箱
git config --global color.ui true                # 命令输出自动着色
```

### 查看配置
```bash
git config --list                                # 列出所有配置
git config --global --list                       # 列出全局配置
git config user.name                             # 查看单个配置项
```

### 编辑配置
```bash
git config -e                                    # 编辑当前仓库配置
git config -e --global                           # 编辑全局配置
```

### 其他配置
```bash
git config --global core.editor "code --wait"   # 设置默认编辑器
git config --global merge.tool vimdiff           # 设置合并工具
git config --global --unset http.proxy           # 移除代理配置
```

---

## 二、创建仓库

### 初始化
```bash
git init                                         # 在当前目录初始化Git仓库
git init newrepo                                 # 在指定目录初始化仓库
```

### 克隆
```bash
git clone <repo>                                 # 克隆远程仓库到当前目录
git clone <repo> <directory>                     # 克隆到指定目录
git clone git://github.com/schacon/grit.git      # GIT协议克隆
git clone https://github.com/user/repo.git       # HTTPS协议克隆
git clone git@github.com:user/repo.git           # SSH协议克隆
```

---

## 三、基本操作

### 添加文件
```bash
git add <filename >                               # 添加指定文件到暂存区
git add .                                        # 添加所有更改到暂存区
```

### 提交
```bash
git commit -m "提交信息"                          # 提交暂存区的更改到本地仓库
git commit --amend -m "新提交信息"                # 修改最后一次提交（用于反复修改）
git commit -am "提交信息"                         # 将add和commit合为一步（仅适用于已跟踪文件）
```

### 查看状态
```bash
git status                                       # 查看当前版本状态
git status -s                                    # 简短状态输出
```

### 查看差异
```bash
git diff                                         # 查看所有未添加至index的变更
git diff --cached                                # 查看所有已添加index但还未commit的变更
git diff HEAD^                                   # 比较与上一个版本的差异
git diff HEAD -- ./lib                            # 比较与HEAD版本lib目录的差异
```

### 删除文件
```bash
git rm <file>                                    # 从工作区和暂存区删除文件
git rm -r *                                      # 递归删除目录下所有文件
git rm --cached <file>                           # 只从暂存区删除，保留工作区文件
```

### 重命名/移动文件
```bash
git mv <源文件> <目标文件>                         # 重命名或移动文件
```

---

## 四、分支管理

### 创建分支
```bash
git branch <branchname>                           # 创建新分支
git checkout -b <branchname>                     # 创建新分支并切换到该分支
git checkout -b <branchname> origin/<branch>     # 从远程分支创建本地跟踪分支
```

### 切换分支
```bash
git checkout <branchname>                        # 切换到指定分支
git checkout -                                   # 切换到上一个分支
```

### 查看分支
```bash
git branch                                       # 列出本地分支
git branch -r                                    # 列出所有远程分支
git branch -a                                    # 列出所有分支（包括远程）
git branch --merged                              # 显示已合并到当前分支的分支
git branch --no-merged                           # 显示未合并到当前分支的分支
```

### 合并分支
```bash
git merge <branchname>                           # 合并指定分支到当前分支
git cherry-pick <commit-id>                      # 合并某个提交的修改
```

### 删除分支
```bash
git branch -d <branchname>                       # 删除分支（已合并的分支）
git branch -D <branchname>                       # 强制删除分支
git push origin --delete <branchname>            # 删除远程分支
```

### 重命名分支
```bash
git branch -m <旧名> <新名>                        # 重命名本地分支
```

---

## 五、远程仓库操作

### 查看远程仓库
```bash
git remote                                       # 查看所有远程仓库别名
git remote -v                                    # 查看远程仓库地址（fetch和push）
```

### 添加远程仓库
```bash
git remote add <别名> <url>                       # 添加远程仓库
```

### 删除远程仓库
```bash
git remote rm <别名>                              # 删除远程仓库关联
```

### 推送
```bash
git push <远程别名> <分支名>                       # 推送到远程仓库
git push -u origin master                         # 推送并设置上游分支
git push --tags                                   # 推送所有标签到远程
```

### 拉取
```bash
git fetch <远程别名>                              # 获取远程分支（不自动合并）
git fetch --prune                                 # 获取远程分支并清除已删除的远程分支
git pull <远程别名> <分支名>                       # 拉取并合并远程分支（相当于fetch+merge）
```

---

## 六、标签管理

### 创建标签
```bash
git tag <tagname>                                # 创建轻量标签
git tag -a <tagname> -m "标签说明"                 # 创建附注标签
git tag -a <tagname> <commit-id> -m "说明"        # 为指定提交创建标签
git tag -s <tagname> -m "说明"                    # 创建带签名的标签
```

### 查看标签
```bash
git tag                                          # 列出所有标签
git show <tagname>                               # 查看标签详情及提交信息
```

### 删除标签
```bash
git tag -d <tagname>                             # 删除本地标签
git push origin --delete <tagname>               # 删除远程标签
```

### 推送标签
```bash
git push origin <tagname>                        # 推送单个标签
git push origin --tags                           # 推送所有标签
```

---

## 七、查看历史

### git log
```bash
git log                                          # 显示提交日志
git log -n <number>                              # 显示最近n条日志
git log --oneline                                # 简洁的一行格式
git log --graph                                  # 图形化显示分支和合并历史
git log --reverse                                # 反向显示（从最早到最新）
git log --stat                                   # 显示简略统计信息
git log -p                                       # 显示提交的补丁（具体更改内容）
git log --author=<作者>                           # 只显示特定作者的提交
git log --since=<时间>                            # 只显示指定时间之后的提交
git log --until=<时间>                            # 只显示指定时间之前的提交
git log --grep=<模式>                            # 只显示包含指定模式的提交消息
git log --no-merges                              # 不显示合并提交
git log --abbrev-commit                          # 使用短提交哈希值
git log --pretty=format:'%h %s'                  # 自定义格式
```

### git blame（代码溯源）
```bash
git blame <文件路径>                               # 查看文件每行的最后修改信息
git blame -L <起始行>,<结束行> <文件路径>           # 查看指定行范围的修改信息
git blame -C <文件路径>                            # 追踪重命名/拷贝的代码
git blame -M <文件路径>                            # 追踪移动的代码
git blame --show-stats <文件路径>                  # 显示每个作者的行数统计
```

---

## 八、撤销与恢复

### 检出（恢复文件）
```bash
git checkout <commit> -- <file>                 # 恢复文件到某个提交版本
git checkout -- <file>                            # 丢弃工作区的修改（恢复到最后一次提交）
git checkout <commit>                             # 切换到某个提交（分离头指针状态）
```

### 重置
```bash
git reset --soft <commit>                        # 保留工作区更改，仅移动HEAD位置
git reset --mixed <commit>                        # 保留工作区更改，重置暂存区（默认）
git reset --hard <commit>                        # 重置工作区、暂存区、HEAD（危险，会丢失修改）
git reset --hard HEAD                            # 将当前版本重置为HEAD（用于merge失败回退）
```

### 撤销提交
```bash
git revert <commit>                              # 创建一个新提交来撤销指定提交的更改
```

### reflog（找回丢失的提交）
```bash
git reflog                                       # 显示所有提交操作记录
git reset --hard HEAD@{n}                        # 恢复到第n次操作的状态
```

---

## 九、暂存操作

### git stash
```bash
git stash                                        # 暂存当前修改，将工作区恢复到HEAD状态
git stash list                                   # 查看所有暂存
git stash show                                   # 查看暂存的内容
git stash show -p stash@{0}                      # 查看第一次暂存的详细内容
git stash apply                                  # 应用最新的暂存（不删除）
git stash apply stash@{0}                        # 应用指定暂存
git stash pop                                    # 应用暂存并删除
```

---

## 十、搜索

```bash
git grep "搜索内容"                               # 在文件中搜索文本
git grep -e '#define' --and -e SORT_DIRENT       # 使用正则搜索
```

---

## 十一、其他命令

```bash
git ls-files                                     # 列出git index包含的文件
git show-branch                                  # 图示当前分支历史
git show-branch --all                            # 图示所有分支历史
git whatchanged                                 # 显示提交历史对应的文件修改
git ls-tree HEAD                                 # 显示某个git对象
git rev-parse <ref>                              # 显示某个ref对应的SHA1哈希值
git gc                                          # 垃圾回收，优化仓库
git fsck                                         # 检查仓库完整性
git remote add origin2 <url>                     # 添加第二个远程仓库
```

---

## 十二、SSH 密钥

```bash
ssh-keygen -t rsa -C "邮箱"                       # 生成SSH密钥
ssh -T git@github.com                            # 测试SSH连接
ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts  # 添加GitHub主机密钥
```

---

## 附录：Git Flow 工作流命令

```bash
# 创建功能分支
git checkout develop
git checkout -b feature/xyz

# 合并功能分支
git checkout develop
git merge feature/xyz
git branch -d feature/xyz

# 创建发布分支
git checkout develop
git checkout -b release/1.0.0

# 合并发布分支
git checkout main
git merge release/1.0.0
git tag -a 1.0.0 -m "Release 1.0.0"
git checkout develop
git merge release/1.0.0
git branch -d release/1.0.0

# 创建热修复分支
git checkout main
git checkout -b hotfix/1.0.1

# 合并热修复
git checkout main
git merge hotfix/1.0.1
git tag -a 1.0.1 -m "Hotfix 1.0.1"
git checkout develop
git merge hotfix/1.0.1
git branch -d hotfix/1.0.1
```
