## git 仓库
### 1. 关联已有文件到远程仓库
```
$git remote add origin [url]
$git pull origin [main/master/分支名称] 
```

### 2. 远程仓库管理

1. `git remote -v`：列出所有远程仓库的名称和对应的 URL。`-v` 选项表示显示详细信息，包括 fetch（拉取）和 push（推送）的 URL。

2. `git remote show <name>`：显示指定远程仓库的详细信息，包括分支信息和跟踪设置。例如：`git remote show origin`。

3. `git remote rename <old> <new>`：重命名远程仓库的名称。例如：`git remote rename old_name new_name`。

4. `git remote remove <name>`：移除指定的远程仓库。例如：`git remote remove origin`。

5. `git remote set-url <name> <newurl>`：更改远程仓库的 URL。例如：`git remote set-url origin https://new.url/repo.git`。

6. `git fetch <name>`：从指定的远程仓库拉取所有分支和标签的更新，但不合并到本地分支。例如：`git fetch origin`。

7. `git pull <name> <branch>`：从指定的远程仓库拉取更新并尝试合并到当前分支。例如：`git pull origin master`。

8. `git push <name> <branch>`：将当前分支的更新推送到指定的远程仓库。例如：`git push origin master`。

## git 扩展
### GIT LFS

- 是一个Git扩展，通过使用指针来引用大文件，而把大文件本身写入一个单独的LFS存储库来对大文件进行版本控制。

- 官网[Git Large File Storage | Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise. (git-lfs.com)](https://git-lfs.com/)
