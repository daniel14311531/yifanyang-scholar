# Minimal Academic Homepage

一个**简约风格的个人学术主页**，纯 HTML / CSS / JavaScript，无框架、无构建步骤，可直接通过 **GitHub Pages** 部署。

## 目录结构

```
scholarwebsite/
├── index.html            # 页面内容（主要编辑这个文件）
├── assets/
│   ├── fonts.css         # 自托管字体的 @font-face 声明（离线，不请求 Google）
│   ├── fonts/            # 字体文件（woff2）+ OFL 许可证
│   │   ├── inter.woff2
│   │   ├── source-serif-4.woff2
│   │   ├── OFL-Inter.txt
│   │   └── OFL-Source-Serif-4.txt
│   ├── style.css         # 样式（改顶部 CSS 变量即可换主题）
│   ├── script.js         # 深色模式切换 + 年份
│   ├── avatar.svg        # 头像占位图（替换成自己的照片）
│   └── cv.pdf            # 放你的 CV（需自行添加）
├── .nojekyll             # 让 GitHub Pages 按原样发布
└── README.md
```

页面**不加载任何外部资源**：字体已本地化，离线可用，也就不存在第三方请求。

## 本地预览

任选一种（在项目根目录执行）：

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .
```

然后浏览器打开 http://localhost:8000

## 需要改的地方

打开 `index.html`，搜索并替换这些占位内容：

| 位置 | 说明 |
| --- | --- |
| `Your Name` | 你的名字 |
| `Ph.D. Student` / 院系 / 学校 | 身份与单位 |
| `you@example.edu` | 邮箱 |
| Google Scholar / GitHub 链接 | 你的主页链接 |
| About / News / Publications / Teaching / Service | 正文内容 |
| `<title>` 与 `og:title` | 浏览器标题、分享卡片标题 |

替换头像：把你的照片（建议正方形，≥400×400）命名为 `avatar.jpg` 放进 `assets/`，
然后把 `index.html` 中的 `assets/avatar.svg` 改成 `assets/avatar.jpg`。

替换 CV：把 PDF 命名为 `cv.pdf` 放进 `assets/` 即可（链接已写好）。

### 换配色

编辑 `assets/style.css` 顶部的变量即可，例如：

```css
:root {
  --accent: #2f5d8a;   /* 主色（链接、高亮） */
  --bg: #ffffff;       /* 背景色 */
  --text: #1a1a1a;     /* 正文字色 */
}
```

### 换字体

字体是**自托管**的，不依赖 Google Fonts：`@font-face` 在 `assets/fonts.css`，
字体文件在 `assets/fonts/`。当前是 Inter（无衬线）+ Source Serif 4（衬线），
两个都是**可变字体**，各一个 woff2 就覆盖了全部字重。

- **只想换成系统字体**：不用动 `fonts.css`，直接改 `assets/style.css` 里的
  `--font-sans` / `--font-serif` 变量即可（建议保留一个衬线兜底）。
- **想换别的网络字体**：把新字体按同样方式放进 `assets/fonts/`，
  在 `assets/fonts.css` 里改 `@font-face`；详细步骤（含如何从 Google Fonts
  取得 woff2 直链、只拉 latin 子集）写在该文件顶部的注释里。
- 若以后要显示中文，需自行加入中文字体或接受回退到系统字体（当前字体只含
  latin 子集）。

> 字体许可证：Inter 与 Source Serif 4 均为 SIL OFL 1.1，允许自托管与再分发。
> 许可证原文随字体一起放在 `assets/fonts/`，**不能删**。

## 部署到 GitHub Pages

### 1. 创建仓库并推送

```bash
cd scholarwebsite
git init
git add .
git commit -m "Initial commit: academic homepage"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

### 2. 开启 GitHub Pages

进入仓库 → **Settings** → **Pages**：

- **Source** 选择 `Deploy from a branch`
- **Branch** 选择 `main`，目录选 `/ (root)`
- 点击 **Save**

等 1–2 分钟后访问：

```
https://<你的用户名>.github.io/<仓库名>/
```

> 💡 如果仓库名就叫 `<你的用户名>.github.io`，访问地址就是
> `https://<你的用户名>.github.io/`（根域名站点）。

### 3. 绑定自定义域名（可选）

1. 在仓库 **Settings → Pages → Custom domain** 填入你的域名，例如 `www.yourname.com`，保存。
2. 在你的域名服务商处添加 DNS 记录：
   - 根域名 `yourname.com` → 4 条 `A` 记录指向 GitHub Pages IP：
     `185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`
   - `www` 子域名 → 一条 `CNAME` 记录指向 `<你的用户名>.github.io`
3. 勾选 **Enforce HTTPS**。
4. GitHub 会自动生成 `CNAME` 文件到仓库根目录，不要删除它。

## 常见问题

- **页面 404**：确认 Settings → Pages 的 Source 分支是 `main`，且 `/ (root)`；改动后需等待 1–3 分钟。
- **样式没生效**：检查 `assets/style.css` 路径大小写是否一致（GitHub Pages 服务器区分大小写）。
- **图标 / 字体不显示**：字体已自托管在 `assets/fonts/`，离线也能正常显示。
  只有 Emoji（如页签图标 🎓）依赖系统字体，属于正常现象。

## License

模板可自由使用与修改（CC0 / MIT 任选）。页面内容版权归你所有。
