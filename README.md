# Roomeo

Roommate type quiz (`quiz.html`) and marketing landing (`index.html`).

## 本地打开网站（推荐给协作者）

不要用 `file://` 直接双击打开（部分资源路径与浏览器策略可能异常）。在项目根目录执行：

```bash
cd Roomeo
python3 -m http.server 8000
```

浏览器访问：**http://127.0.0.1:8000/** 打开首页，点 **Take the quiz** 进入测验。

若已安装 Node.js，也可用：`npx --yes serve -l 8000`。

## 仓库与权限

本仓库在 GitHub 上为 **Private**：只有你邀请的协作者能访问。邀请路径：**GitHub → 仓库 → Settings → Collaborators**。

## 资源目录（简要）

| 路径 | 内容 |
|------|------|
| `assets/brand/` | `logo.svg` |
| `assets/site/` | 首页用图：banner、icons、背景图等 |
| `assets/quiz/questions/` | `quiz cover.png`、`q1.png`–`q12` |
| `assets/characters/` | 各类型小头像 `beaver.png` … |
| `assets/result-hero/` | 结果页顶栏角色层 `turtle.png` …（透明底叠在 hero-room 上） |
| `assets/roommate-type-cards/` | 落地页类型大卡 |
| `assets/quiz-result-1-0/` | 结果页 UI（波浪、徽章、底图等） |
| `docs/` | 产品/设计说明 Markdown（不参与页面加载） |
