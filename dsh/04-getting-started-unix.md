# 第四章：macOS / Linux（Unix）快速上手

[返回教程首页](README.md) · [上一章：Windows 从零开始](03-getting-started-windows.md) · [下一章：进阶、常见问题与参考文献](05-advanced-faq-references.md)

> 本教程以 Windows 为主线（见[第三章](03-getting-started-windows.md)）。如果你用的是 **macOS 或 Linux**，读这一章就够了——流程和 Windows 几乎一样，只是"装 Node.js"和"命令行"这两步不同。

---

## 4.1 和 Windows 流程的对应关系

| 步骤 | Windows（第三章） | macOS / Linux（本章） |
|---|---|---|
| 装 Node.js | 官网下载 `.msi` 安装包 | 见 4.2 节 |
| 打开命令行 | PowerShell | 终端（Terminal） |
| 建工作文件夹 | `cd D:\mywork` | `mkdir ~/mywork && cd ~/mywork` |
| 启动 dsh | `npx @deepseek-ai/dsh web` | **同样的命令**：`npx @deepseek-ai/dsh web` |
| 配置模型 | 网页里操作 | 网页里操作（完全一样） |
| 选择工作区 | 网页里操作 | 网页里操作（完全一样） |
| 派活 | 网页里对话 | 网页里对话（完全一样） |

也就是说：**只有"装 Node.js"和"敲命令的方式"不一样，网页里的操作（配置模型、选工作区、对话、审批）三个系统完全一样**，这里不再重复，直接参考[第三章 3.4 ~ 3.8 节](03-getting-started-windows.md)。

## 4.2 安装 Node.js

### macOS

任选一种：

- **方法 A（官网安装包，最简单）**：打开 [https://nodejs.org/](https://nodejs.org/) [30]，下载 **LTS** 版本的 `.pkg` 安装包，双击安装即可。
- **方法 B（Homebrew，懂一点命令行的话）**：如果你装过 [Homebrew](https://brew.sh/)，在终端里执行：

  ```bash
  brew install node
  ```

### Linux

任选一种：

- **方法 A（官网二进制包）**：从 [https://nodejs.org/](https://nodejs.org/) [29] 下载 LTS 版本的 Linux 二进制包，解压并把 `bin` 目录加入 PATH（方法因发行版而异）。
- **方法 B（nvm，推荐新手）**：nvm 是 Node.js 的版本管理器，一条命令装好还能随时换版本。在终端里执行（详见 nvm 官方说明 [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)）：

  ```bash
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
  ```

  装完重开终端，然后：

  ```bash
  nvm install --lts
  ```

装完后验证（无论哪种系统）：

```bash
node -v
```

看到类似 `v24.x.x` 就成功了 ✅。官方要求 **Node.js 22.19 以上（或 24 以上）** [5]。

## 4.3 启动 dsh

1. 打开**终端**（Terminal）。
2. 建一个工作文件夹并进入：

   ```bash
   mkdir ~/mywork
   cd ~/mywork
   ```

3. 启动（第一次会问是否安装，输入 `y`）：

   ```bash
   npx @deepseek-ai/dsh web
   ```

4. 浏览器会自动打开 `http://127.0.0.1:3080` [1]。如果没有自动打开，就手动输入这个地址。

接下来：**配置模型（3.5 节）→ 选择工作区（3.6 节）→ 派活（3.7 节）**，网页操作和 Windows 完全一样。

## 4.4 Unix 用户专属说明

1. **AI 用的是 bash，不是 PowerShell。** 在 Linux / macOS 上，dsh 挂载的是 bash 命令栈；只有在 Windows 上才是 PowerShell [13]。所以你让 AI "运行一条 shell 命令"时，它用的是 bash。
2. **沙箱（隔离墙）实现不同。** dsh 的进程沙箱在不同系统用不同技术：Linux 用 bwrap/Landlock，macOS 用 Seatbelt，Windows 用 ACL 受限令牌 [10]。你不用管它具体是什么，只需知道：**默认模式下 AI 被限制在工作区内干活**，想让它访问工作区以外的东西会触发审批。
3. **`~/.dsh` 是你的"配置老家"。** 设置文件（`settings.yaml`）、密钥文件（`.credentials.yaml`）都存在 `~/.dsh` 目录下（即 `$DSH_HOME`，默认 `~/.dsh`）[7][27]。想备份配置，备份这个文件夹即可。
4. **SSH 远程使用时浏览器不会自动打开。** 如果你是 SSH 到服务器上跑 dsh，官方说明：SSH 启动时只打印地址、跳过自动打开浏览器，因为本地转发地址由 SSH 客户端持有 [1][32]。你需要在本地浏览器访问转发的地址。

## 4.5 Unix 常见问题速查

| 问题 | 解决办法 |
|---|---|
| `npx: command not found` | Node.js 没装好，回到 4.2 节 |
| 端口被占用 | `npx @deepseek-ai/dsh web --port 8080` [11]，访问 `http://127.0.0.1:8080` |
| 提示权限不足 | 不要用 `sudo` 跑 dsh；把工作文件夹权限改成自己可读写：`chmod -R u+rwX ~/mywork` |
| 防火墙提示 | 本机服务（127.0.0.1）默认只允许本机访问，正常 |

---

**这一章小结：** Unix 上的流程 = 装 Node.js + 终端敲同样的命令，网页操作与 Windows 完全一致。唯一值得记住的区别：Unix 下 AI 用的是 bash，配置存放在 `~/.dsh`。

玩熟了以后，请看[第五章：进阶、常见问题与参考文献](05-advanced-faq-references.md)。
