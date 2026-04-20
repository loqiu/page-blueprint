# 安装说明

这个仓库现在有两种使用形态：

1. **按 skills 安装**
2. **按本地 plugin 安装**

对大多数用户，**按 skills 安装是最快的路径**。

当前文档对应版本：`v0.1.1`

重要分支说明：

- `main`：源码真源开发分支
- `public-skills`：给 `npx skills add ...` 使用的自包含公开安装分支

## 1. 按 skills 安装

使用 Codex 内置的 skill installer，直接从带 tag 的 GitHub 仓库安装。

### Windows

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

### macOS / Linux

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo loqiu/page-blueprint \
  --path skills/page-blueprint skills/page-builder \
  --ref v0.1.1
```

### 安装后

1. 重启 Codex。
2. 先用 `page-blueprint`。
3. 只有在蓝图被批准后，再用 `page-builder`。

### 升级

升级 skills 时，重新执行同一条安装命令，只是把 tag 改成新版本：

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

然后重启 Codex。

### 通过 `npx skills` 公开安装

如果你要走 `skills.sh` / `npx skills` 这条安装链路，请不要直接指向 `main`，而要使用公开分发分支：

```bash
npx skills add https://github.com/loqiu/page-blueprint/tree/public-skills --skill page-blueprint page-builder -g -a codex -y --copy
```

## 2. 按本地 plugin 安装

如果你想使用带这些内容的 plugin 包，就走这条路径：

- `.codex-plugin/plugin.json`
- 插件元数据
- 插件内自包含的 `skills/`
- 插件内自包含的 `shared/`
- 插件图标与资源

### 第一步：把插件目录放到本地

你需要一个本地 plugin 根目录：

- Windows：`%USERPROFILE%\plugins`
- macOS / Linux：`~/plugins`

最终插件路径应为：

- Windows：`%USERPROFILE%\plugins\page-blueprint`
- macOS / Linux：`~/plugins/page-blueprint`

你可以通过两种方式把内容放进去：

- clone 这个仓库，然后拷贝 `plugins/page-blueprint/`
- 从 release 下载 `page-blueprint-plugin-v0.1.1.zip`，解压到这个位置

### 第二步：创建或更新 marketplace.json

如果没有这个文件，就创建：

- Windows：`%USERPROFILE%\.agents\plugins\marketplace.json`
- macOS / Linux：`~/.agents/plugins/marketplace.json`

最小可用内容如下：

```json
{
  "name": "local-marketplace",
  "interface": {
    "displayName": "Local Plugins"
  },
  "plugins": [
    {
      "name": "page-blueprint",
      "source": {
        "source": "local",
        "path": "./plugins/page-blueprint"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Coding"
    }
  ]
}
```

如果你的 marketplace 文件已经存在，只需要把这个 plugin entry 追加到 `plugins[]` 里。

### 第三步：重启 Codex

重启后，Codex 就能通过本地 marketplace 发现这个 plugin。

### 升级

升级本地 plugin 时：

1. 下载最新 release 里的 plugin zip
2. 覆盖本地 `page-blueprint` 目录
3. 重启 Codex

## 该选哪种安装方式

### 适合按 skills 安装

- 想走最短的远程安装路径
- 想通过 GitHub 仓库 + tag 直接安装
- 暂时不需要 plugin marketplace 元数据

### 适合按本地 plugin 安装

- 想使用已经打包好的 plugin 目录
- 想保留插件元数据和 marketplace 接入方式
- 想把这个仓库作为内部本地 Codex plugin 分发
