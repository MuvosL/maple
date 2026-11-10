# 把这个博客变成你自己的

这份文档写给「拿到这个文件夹复制品」的下一个人：把它改成你自己的 Quartz 博客，并发布到 GitHub Pages。

整个流程是纯线上的：

```text
GitHub 网页建仓库 → 本地改配置文件 → git 推送 → GitHub Actions 自动构建 → Pages 发布
```

你本地只需要：一个 GitHub 账号、git，以及写作时用的 Obsidian。**不需要在本地安装 Node、安装依赖或运行构建**——所有构建都发生在 GitHub 的服务器上。

> 下面的命令默认在**仓库根目录**（能看到 `package.json`、`quartz.config.ts` 的那一层）执行。

---

## 0. 开始前准备

| 依赖 | 说明 |
| --- | --- |
| GitHub 账号 | 托管仓库、运行 Actions、发布 Pages |
| git | 本地提交与推送（Windows 装 Git for Windows 即可） |
| Obsidian | 可选，只在写作时需要 |

> 构建环境由仓库自带的 workflow 决定（`.github/workflows/deploy.yml` 里固定使用 Node 22），所以你的电脑上装什么 Node 版本都不影响线上构建。

---

## 1. 第一步：清掉原作者的 git 历史

复制来的文件夹里如果还带着 `.git`，里面是**原作者的提交历史**。直接在这种仓库上继续提交并推送，会把别人的提交记录一起带过去。模板复用的正确做法是重新开始。

### Windows PowerShell

```powershell
Remove-Item -Recurse -Force .git
git init -b main
```

<br />

---

## 2. 第二步：改掉站点身份信息

这一步是必须做的。下面每一条都给出了「文件 → 当前值 → 改成什么」。

| 文件 | 位置 | 当前值 | 改成 |
| --- | --- | --- | --- |
| `quartz.config.ts` | `pageTitle` | `"Maple's Notes"` | 你的站点标题 |
| <br />             | <br />            | <br />| <br />            |
| `quartz.config.ts` | `baseUrl` | `"muvosl.github.io/maple"` | `"你的用户名小写.github.io/仓库名"` |
| <br />             | <br />      | <br /> | <br />          |
| `quartz.layout.ts` | Feedback 组件 `repo` | `"MuvosL/maple"` | `"你的用户名/仓库名"` |
| `quartz.layout.ts` | 页脚 `GitHub` 链接 | `https://github.com/MuvosL/maple` | 你的仓库地址 |
| `.github/workflows/deploy.yml` | release job 的 `if` 条件 | `github.repository == 'MuvosL/maple'` | `'你的用户名/仓库名'` |
| `.github/workflows/deploy.yml` | release 正文里的 Star 链接 | `https://github.com/MuvosL/maple` | 你的仓库地址 |
| `README.md` | 第 1 行标题 | `# Maple's Notes` | `# 你的站点标题` |
| `README.md` | 「在线访问」一行 | `muvosl.github.io/maple` | 你的站点地址（文字和链接都要改） |
| `content/index.md` | 首页正文 | 占位内容（`jiayidian chenshu`、`dfsgsa`） | 你自己的介绍 |

### 2.1 `quartz.config.ts`

```ts
pageTitle: "Maple's Notes",
pageTitleSuffix: "",
analytics: null,
baseUrl: "muvosl.github.io/maple",
```

- `pageTitle`：站点标题，会显示在左上角、浏览器标签页和页面 `<title>` 里。
- `analytics`：当前是 `null`，表示不做访问统计。需要统计时按 `quartz/cfg.ts` 里定义的 provider 填（如 `plausible`、`google`、`umami` 等）；不确定就保持 `null`，不影响构建。

#### `baseUrl` 的格式要求

只写「域名 + 路径」，三条硬性规则：

1. **不带协议**：不要写 `https://`；
2. **不带末尾斜杠**：`alice.github.io/notes`，不是 `alice.github.io/notes/`；
3. **用户名小写**，并带上仓库名前缀。
4. <br />

### 2.2 `quartz.layout.ts`

```ts
Component.Feedback({
  repo: "MuvosL/maple" as `${string}/${string}`,
}),
```

把字符串改成你的 `用户名/仓库名`，**保留后面的 `` as `${string}/${string}` `` 类型断言**，否则 TypeScript 会报错（这个错误会直接让线上构建失败）。

页脚：

```ts
footer: Component.Footer({
  links: {
    GitHub: "https://github.com/MuvosL/maple",
  },
}),
```

改成你的仓库完整地址。

### 2.3 `.github/workflows/deploy.yml`

release job 的触发条件：

```yaml
if: "github.repository == 'MuvosL/maple' && startsWith(github.event.head_commit.message, 'blog: auto publish')"
```

两个条件都要满足才会创建 GitHub Release：

- `github.repository` 必须等于你的 `用户名/仓库名`，不改的话新仓库永远不发 Release（部署本身不受影响）；
- 提交信息必须以 `blog: auto publish` 开头。如果你不打算沿用这个提交习惯，release job 同样不会运行。要么改这个前缀，要么把整个 `release` job 删掉——它只是「发版公告」，和部署无关。（作为参考：这个模板仓库当前的提交信息是 `vault backup: ...` 这种格式，所以原仓库里 release job 实际上也没被触发过。）

同一个文件里，release 正文还有一条 Star 链接：

```yaml
⭐ [Star 仓库](https://github.com/MuvosL/maple)
```

改成你自己的仓库地址。

### 2.4 `README.md`

- 第 1 行是站点标题；
- 第 5 行的「在线访问：[muvosl.github.io/maple](https://muvosl.github.io/maple)」，显示文字和链接都要换成你的站点地址。

### 2.5 `content/index.md`

这是站点首页。当前正文是占位内容（`jiayidian chenshu`、`dfsgsa`），换成你自己的介绍即可。frontmatter 里的 `title: '首页'` 可以保留，也可以改成你想要的首页标题。

### 2.6 不要改动的东西

- `LICENSE.txt`；
- `package.json` 里的上游归属信息（`name`、`author`、`repository`、`homepage`）——这是 Quartz 本身的元信息，不是你的站点身份；
- `quartz/` 目录下的任何内容（主题、组件、插件实现）。

---

## 3. 第三步：建 GitHub 空仓库并首次推送

### 3.1 在 GitHub 上建仓库

- **Repository name** 填你的仓库名（想用根站就填 `你的用户名.github.io`）；
- **不要**勾选「Add a README file」「Add .gitignore」「Choose a license」——本地已经有文件，远程初始化过会冲突；
- 建议选 **Public**：GitHub Pages 对私有仓库需要付费套餐，公开仓库免费；
- 创建后页面上给出的 `https://github.com/用户名/仓库名.git` 就是稍后的远端地址。

### 3.2 在本地提交并推送

xian根目录打开cmd

```bash
git add .
git commit -m "初始化我的博客"
git remote add origin https://github.com/你的用户名/你的仓库名.git
git push -u origin main
```

逐条说明：

- `git add .`：把当前目录（受 `.gitignore` 影响，`public`、`.obsidian` 等不会进版本库）加入暂存区；
- `git commit`：生成你的第一个提交，这条提交里只有你自己的改动；
- `git remote add origin ...`：把本地仓库和 GitHub 上的空仓库关联起来；
- `git push -u origin main`：首次推送并建立上游跟踪，之后直接 `git push` 即可触发线上构建。

<br />

---

## 4. 第四步：开启 GitHub Pages

推送成功后，去仓库的 **Settings** 做两项设置：

1. **Settings → Pages → Build and deployment → Source**：选择 **GitHub Actions**。
   不选这一项，`actions/deploy-pages` 会找不到 Pages 站点，部署步骤失败。
2. **Settings → Actions → General → Workflow permissions**：选择 **Read and write permissions**。
   `deploy.yml` 的 release job 需要 `contents: write` 来创建 Release。

部署完成后的站点地址形态：

| 仓库类型 | 地址 |
| --- | --- |
| 普通仓库 `notes` | `https://用户名.github.io/notes/` |
| 根站 `用户名.github.io` | `https://用户名.github.io/` |

刚部署完可能出现短暂 404 或样式缺失，等 1–2 分钟再刷新即可。

---

## 5. 第五步：线上生效链路（推送到发布）

这一节解释「你推送之后，GitHub 上到底发生了什么」，以及出问题时去哪里看。

### 5.1 链路

```text
git push origin main
        │
        ▼
GitHub Actions：workflow「Deploy Quartz site to GitHub Pages」
        ├─ build job
        │    1. checkout 仓库
        │    2. 安装依赖（npm ci）
        │    3. 构建站点
        │    4. 上传产物（public 目录）
        ├─ deploy job（needs: build）
        │    5. 把产物发布到 GitHub Pages
        └─ release job（needs: deploy，可选）
             6. 满足条件时创建一条 GitHub Release
        │
        ▼
https://用户名.github.io/仓库名/  生效
```

要点：

- 只有推送到 `main` 才会触发（`on.push.branches: [main]`）；
- 构建在 GitHub 的服务器上完成，你的电脑不需要参与，也不需要能运行 Node；
- 每次推送都会重新构建整站，改了配置或笔记都一样；
- 部署成功后通常 1–2 分钟内可访问新内容（可能有 CDN 缓存）。

### 5.2 在哪里看构建日志

1. 打开仓库页面 → 顶部 **Actions** 标签；
2. 左侧选 `Deploy Quartz site to GitHub Pages`；
3. 点进最近一次运行（列表里显示提交信息和状态）；
4. 左侧会列出 `build`、`deploy`（以及可能的 `release`）三个 job，点 job 名展开每一步；
5. 点开某一步即可看到完整日志，右上角可以下载日志或重新运行（**Re-run jobs**）。

### 5.3 失败时怎么看报错

- 运行列表里出现红色叉号，说明该次运行失败；点进去找到带红叉的 **step**，那一步的日志末尾通常就是原因；
- 先看 `build` job 是否失败（大部分问题在这里，比如配置写错、TypeScript 报错、依赖安装失败）；
- `build` 成功但 `deploy` 失败，多半是 Pages 没有按上一节设置好；
- 日志里可以搜 `Error`、`error`、`exit code` 快速定位；末尾形如 `Process completed with exit code N` 的那行就是失败退出码；
- 常见退出码 126 的含义与修复见[常见坑](#7-常见坑)第 1 条；
- 修复后重新 `git push` 即可再次触发，也可以在运行页面点 **Re-run jobs** 重跑同一次提交。

> 关于 `release` job：它只有在「仓库名匹配」且「提交信息以 `blog: auto publish` 开头」时才会创建 Release；不满足条件时它会被跳过（灰色），这不是部署失败。

---

<br />

### 6.6 用 Obsidian Git 插件提交推送

如果想在 Obsidian 里点一下就把笔记推上去，可以启用 Obsidian Git 插件：

1. 这个文件夹的 `.obsidian/plugins/` 里已经带了 **Git** 插件，`community-plugins.json` 里也已列出；打开 vault 后到设置里确认它处于启用状态即可（如果被禁用，去 **Community plugins** 启用）；
2. 插件设置里填好提交用的用户名和邮箱，必要时指定 git 可执行文件路径；
3. 快捷键方面：本文件夹的 `.obsidian/hotkeys.json` 里已经给命令 `obsidian-git:push` 绑定了 **Ctrl+Shift+A**。在 Git 插件 **2.43.0** 中，这个命令 id 对应的就是 **Commit-and-sync**（暂存 + 提交 + 拉取 + 推送）。

<br />
- `.obsidian` 已被 `.gitignore` 忽略，所以插件配置和快捷键**不会**同步到 GitHub，换机器要重新配；
- Commit-and-sync 推送的是当前分支，开始前确认你在 `main` 上；
- 推送完成后，去仓库 **Actions** 看这次运行的状态，就知道线上是否发布成功。

---

