**安装 MySQL（Homebrew 推荐）**

```
brew install mysql
brew services start mysql  # 启动 MySQL 服务
```



**安装 Django 的 MySQL 驱动**

```
brew install python3

pip3 install mysqlclient
```



**使用 root 用户登录**

```
mysql -u root -p
```