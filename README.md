<p align="center">
  <img src="assets/icon.png" width="112" alt="Tiny FTP 图标">
</p>

<h1 align="center">Tiny FTP</h1>

<p align="center">一个小巧的 macOS 原生 FTP 文件传输工具。</p>
<p align="center">双栏浏览 · 匿名连接 · 中文文件名 · 约 0.5 MB</p>
<p align="center">
  <a href="https://github.com/li01452/tiny-ftp/releases/latest">下载最新版</a> ·
  <a href="https://github.com/li01452/tiny-ftp/actions">查看构建</a>
</p>

Tiny FTP 用来在 Mac 和局域网内的手机之间传文件。打开手机文件管理器的 FTP 远程管理，在地址栏输入地址，即可浏览、上传和下载。使用 Swift / SwiftUI 构建，调用 macOS 自带的 curl；运行时无需安装 Xcode、Homebrew 或其他运行环境。

为个人日常使用而做，界面和功能保持简单。

## 下载与安装

**[下载 Apple Silicon 版本](https://github.com/li01452/tiny-ftp/releases/latest/download/TinyFTP-macOS-arm64.zip)**

| 项目 | 说明 |
| --- | --- |
| 系统 | macOS 13 或更高版本 |
| 芯片 | Apple Silicon，包括 M1、M2、M3、M4 等 |
| 已测试环境 | MacBook M1，macOS 15.8 |
| 应用体积 | 约 0.5 MB；下载 ZIP 约 255 KB（v1.1.1） |
| 默认地址 | `ftp://192.168.31.6:2121`，可修改 |
| 认证与编码 | 匿名 FTP、UTF-8 |

1. 下载 ZIP，解压一次得到 **Tiny FTP.app**。
2. 将应用拖入 Mac 的“应用程序”文件夹。
3. 双击打开。

应用尚未使用 Apple Developer ID 签名及公证。如果 macOS 提示“Apple 无法验证”，尝试打开一次后，前往 **系统设置 → 隐私与安全性 → 仍要打开**，按系统提示确认即可。

## 能做什么

- **双栏浏览**：左侧是 FTP 服务器，右侧是本地目录，默认打开“下载”。
- **目录导航**：双击文件夹进入，支持返回上级、刷新、选择本地目录。
- **单文件传输**：上传、下载、进度显示和取消；同名文件覆盖前确认。
- **右键操作**：远程文件可右键下载，本地文件可右键上传。
- **快速找新文件**：默认按修改时间从新到旧排列，点击列标题切换排序；也可按名称和大小排序。
- **原生小图标**：带 Retina 尺寸的双向传输图标，适合 Dock 和访达显示。

## 使用方法

1. 在手机上开启 FTP 远程管理，允许匿名访问；需要上传时同时开启写入权限。
2. 将 Mac 和手机连接到同一可信局域网。
3. 在 Tiny FTP 顶部输入手机显示的 FTP 地址，按回车或点击“连接”。
4. 左侧选远程文件，点“下载”或右键下载；右侧选本地文件，点窗口右下角“上传”或右键上传。
5. 文件会传到另一栏当前打开的目录。

默认地址来自个人使用环境，其他设备应填写自己的地址。FTP 传输不加密，适用于可信局域网。

### 传输边界

每次传输一个普通文件；文件夹用于浏览。下载会先写入临时文件，成功后才替换目标文件。上传直接写入服务器目标文件，取消或断线后可能留下不完整的远程文件，需要重新上传。

## 自行构建

下载 Release 附带的 **TinyFTP-source.zip** 并解压，进入 `TinyFTP` 目录：

```sh
bash build.command
```

构建需要 Apple Command Line Tools，生成的应用位于 `dist/Tiny FTP.app`。这只是开发时的依赖，下载成品应用无需安装。

仓库的源代码工程目前打包存放在 `TinyFTP-source.zip` 中；`Sources/TinyFTP`、测试、图标和构建脚本均在压缩包内。

### 验证

在 Mac 上运行 Swift 测试：

```sh
swift test
```

如果已安装 Python 3，可运行带本地 FTP 测试服务器的完整验证，无需第三方 Python 包：

```sh
python3 verification/ftp_smoke.py --swift
```

v1.1.1 已通过 macOS arm64 云端构建、10 项 Swift 测试和 8 项 FTP 检查，并在个人使用环境中测试通过。

### GitHub Actions

仓库会在提交后自动编译、测试和打包。主分支的构建通过后，会根据应用版本号发布尚不存在的 GitHub Release，附带应用、源码和 SHA-256 校验文件；已有版本不会被覆盖。

## 反馈

如遇到连接、文件名或传输问题，可以在 [Issues](https://github.com/li01452/tiny-ftp/issues) 中提供 macOS 版本、手机 FTP 服务来源和完整报错。
