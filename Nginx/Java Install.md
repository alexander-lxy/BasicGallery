## Java 安装配置

**Homebrew安装**

```bash
brew install openjdk

sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk //把homebrew安装的openjdk软链接到系统目录
```





**配置Java环境变量**

在终端中配置环境变量，以便系统能识别`java`和`javac`命令。

- 编辑配置文件

  打开终端，使用编辑器打开配置文件（例如`.zshrc`或`.bash_profile`，取决于你使用的shell）：

  ```bash
  nano ~/.zshrc  # macOS 从 macOS Catalina（10.15）开始，使用 Zsh 作为默认 shell Zsh shell 的配置文件
  ```

  或者：

  ```bash
  nano ~/.bash_profile  # 如果使用bash shell
  ```

  #### 

**配置Java路径**

```bash
export JAVA_HOME=$(/usr/libexec/java_home)
export PATH=$JAVA_HOME/bin:$PATH
```

`/usr/libexec/java_home` 是自动检测当前安装的Java版本的命令。不写进去也没关系。



**生效**

```bash
source ~/.zshrc  # 如果使用zsh shell
```

或者：

```bash
source ~/.bash_profile  # 如果使用bash shell
```



**验证安装**

在终端中运行以下命令，检查Java是否正确安装：

```bash
java -version
javac -version
```



**设置默认Java版本**

如果你安装了多个Java版本，可以使用以下命令切换默认版本：

```bash
/usr/libexec/java_home -v 1.8   # 例如，选择Java 8
```

可以在`.zshrc`或`.bash_profile`中添加类似以下行来永久设置Java版本：

```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)
```

这样，你就完成了在Mac上安装和配置Java的步骤！