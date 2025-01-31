- 以下是你描述的过程的清晰解释和分解：

  1. **通过 Homebrew 安装 Git：** 要通过 Homebrew 安装 Git，可以使用以下命令：

     ```
     brew install git
     ```

  2. **确保 Homebrew 路径优先于系统路径：** 安装 Git 后，你需要确保通过 Homebrew 安装的版本优先于系统预装的版本（例如 macOS 上的默认版本）。你可以通过修改 `PATH` 环境变量来实现：

     ```
     export PATH="/usr/local/bin:/opt/homebrew/bin:$PATH"
     ```

     这条命令确保 `/usr/local/bin` 和 `/opt/homebrew/bin`（Homebrew 安装软件的路径）会被优先检查，从而确保终端使用的是通过 Homebrew 安装的 Git 版本。

  3. **加载新的配置文件：** 修改了 `.zshrc`（对于 Zsh shell）或 `.bashrc`（对于 Bash shell）后，需要重新加载它以应用更改：

     ```
     source ~/.zshrc  # 或者 source ~/.bashrc
     ```

  ### 根据 `which git` 输出的不同情况：

  - **输出 `/usr/bin/git`：**
     这意味着你正在使用 macOS 系统默认提供的 Git 版本（通常是 Apple 提供的版本），它可能是一个过时的版本，或者比 Homebrew 版本要旧。
  - **输出 `/usr/local/bin/git`：**
     这表示你正在使用通过 Homebrew（或手动）安装的 Git 版本，通常这是从官方 Git 仓库获取的最新稳定版本。
  - **输出 `/opt/homebrew/bin/git`：**
     在 Apple Silicon 芯片（M1/M2）上，Homebrew 会将软件安装到 `/opt/homebrew/bin`，如果看到这个路径，说明 Git 是通过 Homebrew 安装的，适用于 Apple Silicon。

  ### `export` 的解释：

  - `export` 是一个 Shell 命令，用于将环境变量导出，使得它在子进程中也能使用。在这里，它用来修改 `PATH` 环境变量，并将其导出，使得当前终端和所有子进程都能识别这个修改。
  - 修改后的 `PATH` 确保像 `/usr/local/bin` 和 `/opt/homebrew/bin` 这样的目录会被优先检查，从而让 Homebrew 安装的 Git 版本优先于系统自带的 Git。

  