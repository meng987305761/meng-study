# MEM 考研学习目标工作台 · 手机 App 化部署指南

本目录是一套可安装到手机主屏、像 App 一样使用的 **PWA（渐进式 Web 应用）** 文件包。

```
meng-study-app/
├── index.html              # 主程序（已升级为可安装的 App 壳）
├── manifest.webmanifest    # 应用清单（名称/图标/全屏模式）
├── sw.js                   # 离线缓存 Service Worker
├── icon-192.png            # 主屏图标（Android）
├── icon-512.png            # 高清图标 / 启动图
└── apple-touch-icon.png    # 主屏图标（iOS）
```

> 为什么不能直接用原来那条 workbuddy.link 链接当 App？因为那只是**单个网页**，没有图标清单、无法全屏、断网就打不开。本包补齐了这些能力。

---

## 一、部署（任选其一，约 3 分钟）

PWA 需要 **HTTPS 网址**才能安装，所以先把整个文件夹传到一个静态托管平台。

### 方案 A：GitHub Pages（有 GitHub 账号，最稳）
1. 新建一个仓库（如 `meng-study`），用 Git 连带 `gh` 推送即可（我也可以帮你做）。
2. 仓库 **Settings → Pages → Source 选 main 分支 / root**，保存。
3. 稍等 1 分钟，得到网址 `https://<你的用户名>.github.io/meng-study/`。

### 方案 B：Netlify Drop（拖拽即得网址）
1. 打开 https://app.netlify.com/drop
2. 把本目录（或 `meng-study-app.zip`）直接拖进页面。
3. 立即得到一条 `https://xxxx.netlify.app` 网址。

### 方案 C：任意静态托管 / 对象存储 / 自有服务器
把 6 个文件放在同一目录、通过 HTTPS 提供即可（Nginx、OSS/COS + CDN、Vercel、Cloudflare Pages 都行）。
注意：**目录结构不能改**，`index.html` 必须能通过根路径访问。

---

## 二、安装到手机主屏

> 关键：必须用**系统自带浏览器**打开（iOS 用 Safari，Android 用 Chrome/Edge）。**微信内置浏览器不支持安装**。

### iPhone / iPad（Safari）
1. Safari 打开你的网址。
2. 点底部 **分享 ⬆️** 按钮。
3. 选择 **「添加到主屏幕」→ 添加**。
4. 桌面出现「MEM考研」图标，点开即为**全屏无地址栏**的 App。

### Android（Chrome / Edge）
1. Chrome 打开网址。
2. 右上角 **⋮ 菜单** → **「安装应用」** 或 **「添加到主屏幕」**。
3. 确认后桌面生成 App 图标（部分机型会弹出"安装"横幅，直接点即可）。

---

## 三、使用与数据说明

- **打卡数据**存在手机本地（`localStorage`），**不同网址/不同设备之间不互通**。
- 换手机或换网址时，用页面顶部 **「导出 JSON 备份」** 保存，再在新设备 **「导入恢复」**。
- **离线可用**：首次联网打开后即自动缓存，之后没网也能正常打卡。
- **更新内容**：替换文件重新上传即可；若页面逻辑有更新，请同时把 `sw.js` 里的 `CACHE = 'meng-study-v1'` 改成 `v2`、`v3`…，以触发缓存刷新。

---

## 四、更省事的替代方案（不做 PWA）

如果不想折腾托管，直接**用手机浏览器打开原 workbuddy.link 链接 → 加入主屏/收藏**，也能得到图标入口，纯在线使用（无全屏、无离线）。
