

**删除 Flutter 的 `bin` 目录**

export PATH=$(echo $PATH | sed 's/:\/Users\/username\/flutter\/bin//g')



```
# 列出 PATH 中的每个目录
echo $PATH | tr ':' '\n'
```



```
# 检查 Flutter 的路径
which flutter
```



