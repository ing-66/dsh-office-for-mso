# dsh-office-for-mso 安装说明（WorkBuddy / DeepSeek Harness）

本仓库是 `Mikuzjc/dsh-office-for-mso` 的公开 Fork。这是社区项目，通过本地桥接服务和 Office.js 加载项操控正在打开的 Microsoft Word、Excel、PowerPoint；不支持 WPS。

## 先安装桥接服务和 Office 加载项

要求 Node.js 18+ 与 Microsoft Office 桌面版。Windows 推荐在仓库根目录执行：

```powershell
npm run setup
```

该命令会注册登录自启计划任务并安装 Office 加载项，可能触发 UAC。执行前应审阅 `package.json`、`install.ps1` 和 `manifest.xml`。安装后重新打开 Office 文档，并保持“DSH Office 执行器”窗格开启。

## 安装到 WorkBuddy

桥接服务安装完成后，把调用说明复制到 WorkBuddy：

```powershell
New-Item "$HOME\.workbuddy\skills\office-bridge" -ItemType Directory -Force | Out-Null
Copy-Item '.\skills\office-bridge\SKILL.md' "$HOME\.workbuddy\skills\office-bridge\SKILL.md" -Force
```

重启 WorkBuddy。只复制 `SKILL.md` 不会安装桥接服务或 Office 加载项；两部分必须同时就绪。

## 安装到 DeepSeek Harness

按上游当前约定复制到 DSH 使用的 Agent Skill 根目录：

```powershell
New-Item "$HOME\.agents\skills\office-bridge" -ItemType Directory -Force | Out-Null
Copy-Item '.\skills\office-bridge\SKILL.md' "$HOME\.agents\skills\office-bridge\SKILL.md" -Force
```

重启 DSH，然后先检查 `http://127.0.0.1:3000/office/status` 与 Office 窗格是否在线。该项目不是微软官方产品。

官方上游：<https://github.com/Mikuzjc/dsh-office-for-mso>

