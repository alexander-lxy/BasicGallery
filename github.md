## Git命令

**初始化新的 Git 仓库**：

```bash
git init
```

- 该命令会在当前目录下创建一个新的 `.git` 文件夹，标志着该目录成为一个 Git 仓库。

**添加所有修改的文件**：

```bash
git add .
```

- `git add .` 会将当前目录下所有已修改和新增的文件添加到暂存区，准备提交。注意：这个命令会添加所有修改过的文件，包括无意间修改的文件。

**提交修改到本地仓库**：

```bash
git commit -m "initial commit"
```

- `git commit -m` 用于将暂存区的文件提交到本地 Git 仓库，并附上提交信息。提交信息 `"initial commit"` 说明这是第一次提交。

**添加远程仓库 URL**：

```bash
git remote add origin https://github.com/alexander-lxy/AndroidGallery.git
```

- 这个命令会将远程仓库添加为 `origin`，并使用 HTTPS 地址。远程仓库是托管在 GitHub 上的代码库，使用这个 URL 进行同步。

**将远程仓库的 URL 改为 SSH**：

```bash
git remote set-url origin git@github.com:alexander-lxy/AndroidGallery.git
```

- 如果您希望通过 SSH 协议与 GitHub 通信，可以使用这个命令将远程仓库的 URL 从 HTTPS 修改为 SSH。SSH 连接方式不需要输入用户名和密码，前提是您已经设置了 SSH 密钥。

**查看远程仓库的 URL**：

```bash
git remote -v
```

- 这个命令会列出与当前 Git 仓库关联的所有远程仓库及其 URL。如果仓库关联了多个远程地址（例如 `origin` 和 `upstream`），都可以查看。

**查看本地、远程分支**：

- 本地分支：

```bash
git branch
```

- 远程分支：

```bash
git branch -r
```

- 所有分支（本地和远程）：

```bash
git branch -a
```

- `git branch` 显示本地分支，`git branch -r` 显示远程分支，`git branch -a` 显示所有分支。

**强制推送到远程仓库的 `main` 分支**：

```bash
git push origin master:main --force
```

- `git push` 会将本地的分支推送到远程仓库。使用 `--force` 强制推送会覆盖远程仓库中的内容，注意：使用这个命令时需要小心，因为它会覆盖远程分支的历史记录。





## Git安装

**安装Homebrew**

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**安装Git**

```undefined
brew install git
```

**创建ssh key**

```csharp
git config --global user.name "alexander"
git config --global user.email "alexander_lxy@outlook.com"
```

- Secure Shell Key 公钥 (Public Key): 这是可以公开的密钥，通常将它添加到你要连接的服务器上的 `~/.ssh/authorized_keys` 文件中。公钥用于加密数据。**私钥 (Private Key)**: 私钥是保密的，只应存储在客户端计算机上，用来解密数据。只有拥有相应私钥的人才能通过公钥进行身份验证。





## github 配置

**配置SSH**

```bash
cd ~/.ssh & ls
```

- `cd ~/.ssh`：切换到用户的 `.ssh` 目录，`~` 代表用户的主目录。
- `ls`：列出 `.ssh` 目录中的文件。

**生成密钥**

```bash
ssh-keygen -t rsa -b 4096 -C "alexander_lxy@outlook.com"
```

- `-t rsa`：指定密钥类型为 `rsa`。
- `-b 4096` 表示密钥长度为 4096 位。
- `-C 'alexander_lxy@outlook.com'`：为生成的密钥添加注释，方便以后识别。

```bash
cat id_rsa.pub
```

- 显示 `id_rsa.pub` 文件内容，即公钥，可以将其添加到 GitHub 账户中以允许 SSH 连接。

**测试 SSH 是否成功连接**

```
 ssh -T git@github.com
```

- You've successfully authenticated, but GitHub does not provide shell access。可以用 SSH 来克隆（clone）仓库、推送（push）代码、拉取（pull）代码

 **Git 凭证保存**

```bash
git config --global credential.helper store
```

- 将 Git 凭证保存在 `.git-credentials` 文件中，这样下次使用 Git 时就不需要再次输入用户名和密码。

**注解说明**：

- 主目录位置：
  - Linux/macOS：`/home/username`
  - Git Bash：`C:\Users\username`
- `~` 代表用户的主目录。
- `~/` 指主目录下的某个文件或子目录。



