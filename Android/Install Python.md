#### brew安装python

```
brew install python@3.13.1
```





#### `pyenv` 管理 Python 版本

**Python无法识别具体版本**

**安装 `pyenv`**

```
brew install pyenv
```

**配置 Shell**

```
# 对于 zsh（macOS 默认）
echo 'eval "$(pyenv init --path)"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
```

**安装 Python 3.13.1**

```
pyenv install 3.13.1       # 安装指定版本
pyenv global 3.13.1        # 设为全局默认版本
```

**验证**

```
python --version  # 显示 3.11.6
which python      # 路径类似 ~/.pyenv/shims/python
```