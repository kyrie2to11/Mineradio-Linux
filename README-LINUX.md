# Mineradio Linux 移植说明

本仓库的 `main` 分支在官方 [XxHuberrr/Mineradio](https://github.com/XxHuberrr/Mineradio) `main` 的基础上,添加了 Linux 打包配置与自动同步构建,由 [jade2-fff/Mineradio-for-linux](https://github.com/jade2-fff/Mineradio-for-linux) 的移植方案启发(该仓库停留在 1.1.1)。

## 包含的改动

- `package.json`:新增 `build:linux` 脚本与 `linux` / `deb` / `appImage` 打包配置(deb + AppImage, x64)
- `.github/workflows/sync-build-linux.yml`:自动同步构建(见下)

上游代码本身对非 Windows 平台已有完善的 `process.platform` 守卫,无需改动业务代码;`build/after-pack.js` 的 rcedit 图标注入也只在 win32 目标执行。

## 自动同步构建

Workflow 每天 04:23(北京时间)运行:

1. 拉取 upstream `XxHuberrr/Mineradio` 的 `main` 并合并进本分支
2. 有新提交则推送,更新 fork 的 `main`
3. 检测 `package.json` 版本号;若 `linux-v<version>` release 尚不存在,则构建 deb + AppImage 并发布 release
4. 版本没变(上游只是小改动)则只同步不构建

手动操作:

- **强制重新构建**:Actions → Sync upstream & build Linux → Run workflow,勾选 `force_build`
- **合并冲突**:若上游改动了 `package.json` 的打包段导致自动合并失败,workflow 会挂掉;本地解决冲突后推送 `main` 分支即可恢复

## 本地构建

```bash
npm ci
npm run build:linux   # 产物在 dist/(deb + AppImage)
```

安装 deb:`sudo apt install ./Mineradio-<version>-amd64.deb`(装到 `/opt/Mineradio`)。

若安装后双击无反应(chrome-sandbox 权限问题):

```bash
sudo chown root:root /opt/Mineradio/chrome-sandbox && sudo chmod 4755 /opt/Mineradio/chrome-sandbox
```
