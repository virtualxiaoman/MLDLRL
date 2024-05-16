<h3>git常用操作命令：</h3>

- 连接远程仓库：`git remote add origin <url>`
- 添加本地文件：`git add <file_name>`
- 提交commit：`git commit -m "msg"`
- 推送到远程仓库：`git push origin main` (假设branch_name是main)
- 拉取远程仓库的更新：`git pull origin main`

额外的，
- 添加全部文件：`git add .`
- 只添加已存在的文件：`git add -u`

</br>

<h3>git常用状态命令：</h3>

- 查看仓库状态：`git status`
- 列出所有分支：`git branch -a`
- 切换分支：`git checkout -b <branch_name>`