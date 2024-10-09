#### github 配置

cd ~/.ssh & ls

ssh-keygen -t rsa -C 'alexander_lxy@outlook.com'   -t秘钥类型为rsa；-C添加邮件注释，方便识别

cat id_rsa.pub

ssh -T git@github.com 测试 SSH 是否能够成功连接到 GitHub

