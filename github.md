#### github 配置

cd ~/.ssh & ls

ssh-keygen -t rsa -C 'alexander_lxy@outlook.com'   -t秘钥类型为rsa；-C添加邮件注释，方便识别

cat id_rsa.pub

ssh -T git@github.com 测试 SSH 是否能够成功连接到 GitHub

git config --global credential.helper store 凭证会保存到 `.git-credentials` 文件中



注：

主目录位于/home/username(linux/macOS) ，C:\Users\username(gitbash)

`~` 就表示用户的主目录；**`~/`**：主目录下的某个文件或子目录
