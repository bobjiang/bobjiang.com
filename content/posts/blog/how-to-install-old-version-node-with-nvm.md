---
Title: 如何安装旧版本的node 在新芯片M1苹果
Date: 2021-01-20
URL: /how-to-install-old-version-node-with-nvm/
tags: [苹果M1芯片, node, nvm]
---

本文记录了自己如何在苹果M1芯片的笔记本上安装旧版本的node (node v14.10.0)

主要分为以下几个过程：

- 脚本安装 `nvm`，不要用brew安装
- 设置 `zshrc` 环境变量
- 安装旧版本 node

# 安装 nvm

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash`

参考 [nvm github repo](https://github.com/nvm-sh/nvm)

# 修改环境变量

nvm 安装后默认更新的是 `bash` 环境变量。MacOS很多采用的默认 `zsh`
因此把 bash 中关于 nvm 的变量部分，增加到 `.zshrc` 中

```
vi ~/.zshrc

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

```

# 安装旧版本 node

```
# start a shell under Rosetta 2.
arch -x86_64 zsh
nvm install v14.10.0
```

参考 [github nvm issue](https://github.com/nvm-sh/nvm/issues/2350)
