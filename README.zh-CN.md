# git-branches

简体中文 | [English](./README.md)

交互式 Git 分支管理工具 —— 浏览、搜索、创建、删除、切换分支，同时展示分支描述。

![zsh](https://img.shields.io/badge/shell-zsh-blue)
![i18n](https://img.shields.io/badge/i18n-zh%20%7C%20en-green)

## 为什么需要它

`git branch` 列出一堆名字 —— `fix-login`、`temp`、`feature-xx-v2` —— 没有上下文，不知道哪个是干什么的，也不知道上次用是什么时候。你明明记得昨天在改一个分支，但在三十个分支里根本找不到。切换要手打完整分支名，清理要一个一个 `git branch -d`。

**git-branches** 用一个交互界面替代这套流程：

- 分支按**最近使用时间排序**，刚用过的永远在最上面。
- 每个分支旁边直接显示**描述信息** —— 不用猜 `feature-auth-refactor` 到底是什么。
- 一个按键就能**切换**、**搜索**、**新建**或**批量删除**。

它只是一个 shell 脚本，除了 zsh 和 git 之外零依赖，一条 `curl` 命令就装好。如果你每天都要在分支间来回切换，它能帮你省下实实在在的时间。

## 功能

- **按最近使用排序** —— 最近 checkout 过的分支排在最前面（通过 `git reflog` 解析）
- **内联展示描述** —— 在分支名旁直接显示 `git branch --edit-description` 设置的描述
- **实时搜索** —— 按 `/` 输入关键词，按分支名和描述实时过滤
- **创建分支** —— 按 `c` 新建分支并直接输入描述
- **删除分支** —— 按 `d` 删除单个分支，或用 `Space` 标记多个分支批量删除
- **编辑描述** —— 按 `r` 调用 `$EDITOR` 编辑选中分支的描述
- **纯键盘操作** —— 支持 `j`/`k`、方向键和单键快捷操作
- **多语言** —— 默认中文，支持英文，自动识别系统语言

## 安装

一行命令安装（同样适用于更新）：

```bash
curl -fsSL https://raw.githubusercontent.com/cyysilver/git-branches/main/git-branches -o /usr/local/bin/git-branches && chmod +x /usr/local/bin/git-branches
```

> 如果 `/usr/local/bin` 需要权限，在命令前加 `sudo`，或安装到用户目录：
>
> ```bash
> curl -fsSL https://raw.githubusercontent.com/cyysilver/git-branches/main/git-branches -o ~/.local/bin/git-branches && chmod +x ~/.local/bin/git-branches
> ```

脚本遵循 `git-xxx` 命名规范，安装到 `PATH` 后自动注册为 **git 子命令**：

```bash
git branches
```

### 别名配置（可选）

在 `~/.zshrc` 或 `~/.bash_profile` 中添加短别名：

```bash
alias br='git-branches'
alias branches='git-branches'
```

三种调用方式：

| 命令 | 说明 |
|------|------|
| `br` | 最短，2 个字符 —— 日常推荐 |
| `branches` | 完整语义 |
| `git branches` | git 子命令风格（无需别名） |

### 其他方式：克隆仓库

```bash
git clone https://github.com/cyysilver/git-branches.git ~/tools/git-branches
export PATH="$PATH:$HOME/tools/git-branches"  # 添加到 shell 配置文件
```

## 使用

进入任意 git 仓库目录，执行：

```bash
git branches    # 或: br / branches
```

### 语言设置

界面语言会自动识别系统 locale，默认中文。如需手动指定：

```bash
# 强制英文
export GIT_BRANCHES_LANG=en

# 强制中文（默认）
export GIT_BRANCHES_LANG=zh
```

## 快捷键

| 按键 | 功能 |
|------|------|
| `j` / `↓` | 向下移动 |
| `k` / `↑` | 向上移动 |
| `Enter` | 切换到选中的分支 |
| `Space` | 标记/取消标记分支（多选） |
| `/` | 搜索/过滤分支 |
| `c` | 创建新分支（附带描述输入） |
| `d` | 删除选中分支，或删除所有标记的分支 |
| `r` | 编辑选中分支的描述（打开 `$EDITOR`） |
| `Esc` | 取消当前操作 / 清除标记 / 退出 |
| `q` | 退出 |

## 分支描述说明

Git 原生支持为分支添加描述：

```bash
git branch --edit-description <分支名>
```

描述信息存储在 `.git/config` 中的 `branch.<name>.description` 字段。本工具读取并内联展示这些描述，方便记忆每个分支的用途。

## 环境要求

- **zsh**（macOS 默认 shell，其他系统可通过包管理器安装）
- **git** ≥ 2.0

## 许可证

MIT
