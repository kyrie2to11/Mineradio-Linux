# Mineradio Linux

[Mineradio](https://github.com/XxHuberrr/Mineradio-paused) 的 Linux 适配 fork，自用为主，欢迎取用。本仓库在 `main` 分支维护 Linux 打包配置和运行修复，提供 **x86_64 的 deb 与 AppImage** 安装包。

Mineradio 是一款融合音乐播放、歌词舞台、粒子视觉与 3D 歌单架的沉浸式音乐播放器。本仓库专注于 Linux；Windows、macOS、Android 和网页版请前往 [Mineradio 官网下载页](https://mineradio.cn/download.html)。

## 下载与安装

前往本仓库的 [Releases](https://github.com/kyrie2to11/Mineradio-Linux/releases)，选择最新 `linux-v*` 版本的附件。请下载与你的系统对应的安装包，不要下载源码压缩包代替安装包。

### Ubuntu / Debian

下载 `Mineradio-<版本>-amd64.deb`，在下载目录中安装（将版本号替换为实际文件名）：

```bash
sudo apt install ./Mineradio-<版本>-amd64.deb
```

程序安装到 `/opt/Mineradio`，可通过应用菜单启动。

### AppImage

下载 `Mineradio-<版本>-x64.AppImage`，添加执行权限后运行：

```bash
chmod +x Mineradio-<版本>-x64.AppImage
./Mineradio-<版本>-x64.AppImage
```

AppImage 无需安装；实际文件名请以 Release 附件为准。

## 更新

Linux 版请从[本仓库 Releases](https://github.com/kyrie2to11/Mineradio-Linux/releases) 获取新版 deb 或 AppImage。应用内的更新入口沿用上游配置，不作为本 fork 的 Linux 更新渠道。

GitHub Actions 每天北京时间 **04:23** 尝试合并上游 `main`，保留 Linux 适配改动；当对应 `linux-v<版本>` 标签尚不存在时，自动构建并发布安装包。推送 `main` 或手动运行工作流也会触发检查。同版本已有标签时，默认跳过构建。

上游目前声明长期停更；自动同步不代表上游会持续发布新版。若同步产生冲突，需要手动解决后才能继续。

## 本地运行与构建

建议使用 Node.js 22，与自动构建环境一致。

```bash
npm ci
npm start
```

构建 Linux 安装包：

```bash
npm run build:linux
```

产物位于 `dist/`，包括 deb 与 AppImage，目前打包目标为 x86_64。

## Linux 适配说明

- 增加 Linux 打包配置、桌面入口和 deb 依赖声明。
- 非 Windows 平台使用 ANGLE GL 后端，避免使用 Windows 专属的 Direct3D 11 后端。
- 在 `main` 分支自动合并上游更新，并构建 Linux 安装包。

Windows 专属的桌面集成功能不应视为 Linux 版的功能承诺。更多维护与构建细节见 [README-LINUX.md](README-LINUX.md)。

## 反馈

Linux 安装、启动或打包问题请提交到[本仓库 Issues](https://github.com/kyrie2to11/Mineradio-Linux/issues)，并附上发行版、桌面环境、软件版本与终端报错。

## 致谢与授权

Mineradio 原项目由 **XxHuberrr** 及其贡献者开发；本仓库维护 Linux 适配。移植方案受到 [jade2-fff/Mineradio-for-linux](https://github.com/jade2-fff/Mineradio-for-linux) 启发。

Copyright (C) 2026 XxHuberrr. 本项目沿用 GPL-3.0 授权，详见 [LICENSE](LICENSE) 和 [NOTICE.md](NOTICE.md)。Mineradio 名称、标识及原创视觉表达的权利归原作者所有。

隐私说明见 [PRIVACY.md](PRIVACY.md)。请遵守第三方音乐平台的服务条款与版权规则。
