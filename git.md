<h3>git常用操作命令：</h3>

- 初始化：`git init`
- 连接远程仓库：`git remote add origin <url>` (url后缀是`.git`)
- 添加本地文件：`git add <file_name>`
- 提交commit：`git commit -m "msg"`
- 推送到远程仓库：`git push origin main` (假设branch_name是main)
- 拉取远程仓库的更新：`git pull origin main`

额外的，
- 添加全部文件：`git add .`
- 只添加已存在的文件：`git add -u`
- 删除git管理但不删除本地文件：`git rm --cached <file_name>`

</br>

<h3>git常用状态命令：</h3>

- 查看仓库状态：`git status`
- 列出所有分支：`git branch -a`
- 切换分支：`git checkout -b <branch_name>`

</br>

<h3>git常用查看命令：</h3>

- 查看提交历史：`git log`
- 查看文件差异：`git diff <file_name>`
- 查看文件修改记录：`git blame <file_name>`
- 查看远程仓库地址：`git remote -v`

</br>

<h3>git常用分支操作：</h3>

- 创建分支：`git branch <branch_name>`
- 删除分支：`git branch -d <branch_name>`
- 合并分支：`git merge <branch_name>`
- 重命名分支：`git branch -m <new_branch_name>`
- 查看分支合并情况：`git branch --merged`

</br>

<h3>git常见报错：</h3>

- `fatal: unable to access 'https://github.com/*****': HTTP/2 stream 1 was not closed cleanly before end of the underlying stream`：
  - 解决方法：`git config --global http.version HTTP/1.1`

- `fatal: refusing to merge unrelated histories`：
  - 解决方法：
    - `git pull origin main --allow-unrelated-histories`
    - 然后在vscode里可以看到冲突的文件(带有红色感叹号)，手动解决冲突(选择保留哪个版本)后再正常提交即可。

- `error: failed to push some refs to `
  - 解决方法：
    - 一般是因为开了代理，使用下面的代码设置代理。请注意，IP和端口号根据自己的代理设置进行修改，`clash`默认端口号是`7890`：
```bash
git config --global http.proxy http://127.0.0.1:7890 
git config --global https.proxy http://127.0.0.1:7890
```

