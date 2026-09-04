# 凌云社官方网站（框架）

基于 VitePress 的社团网站 **纯框架**，默认主题、零内容：

- 不含任何社团信息（无人员名单、无公告内容、无联系方式、无示例数据），
  所有内容由「管理后台」维护后发布。
- 保持 VitePress 默认主题与布局，仅注入一套动效样式（不改布局结构）。

## 快速开始

```bash
npm install
npm run dev      # 本地开发，默认 http://localhost:5173
npm run build    # 构建到 docs/.vitepress/dist
npm run preview  # 预览构建产物
```

> 若 `npm install` 环境受限，可使用 `npm install --ignore-scripts`
> （本项目依赖没有必须执行的安装脚本）。

## 页面模块

| 路径        | 模块       | 说明                       |
| ----------- | ---------- | -------------------------- |
| `/`         | 首页       | 默认 home 布局，模块入口   |
| `/intro`    | 社团介绍   | 章节列表，后台维护         |
| `/showcases`| 成果展示   | 卡片网格，后台维护         |
| `/projects` | 开源仓库   | 仓库卡片，后台维护         |
| `/news`     | 公告动态   | 公告列表（可展开正文）     |
| `/join`     | 加入我们   | 招新说明与联系方式，后台维护 |
| `/admin`    | 管理后台   | 登录后增删改全部模块内容   |

## 管理后台

- 入口：导航栏「管理后台」或直接访问 `/admin`。
- 默认密码：`admin123`，登录后在「账号设置」中修改。
  （前端密码仅为演示用途，不构成真正的安全防护。）
- 公告模型与参考 JavaBean 同构（见 `docs/.vitepress/client/models.js`）：
  `Announcement` 持有 `id / title / author / content`，
  方法 `add()` 添加公告、`write()` 写公告正文、`del()` 删除公告。
- 介绍 / 成果 / 仓库 / 招新模块同样提供增删改。

### 数据发布流程（静态 JSON 数据文件 + 重新构建）

1. 在管理后台完成增删改（自动暂存在浏览器 localStorage）。
2. 「数据发布」→「导出数据文件」，得到 `site-data.json`。
3. 用该文件替换 `docs/.vitepress/data/site-data.json`。
4. 重新执行 `npm run build` 并部署 `docs/.vitepress/dist`。

「导入数据文件」可把导出的 JSON 重新载入继续编辑；
「重置为仓库数据」放弃本地暂存，回到仓库中的数据文件。

## 动画

- 所有自定义组件带入场 / 悬浮 / 按压 / 列表增删 / 弹窗 / 手风琴展开 / Toast 过渡动画。
- 动效样式集中在 `docs/.vitepress/theme/styles/animations.css`。
- 尊重系统「减少动态效果」偏好（`prefers-reduced-motion`）。

## 目录结构

```
docs/
├── index.md                 # 首页
├── intro.md / showcases.md / projects.md / news.md / join.md / admin.md
└── .vitepress/
    ├── config.mts           # 站点与导航配置（无内容数据）
    ├── data/site-data.json  # 站点数据唯一来源（默认全空）
    ├── theme/
    │   ├── index.ts         # 原样导出默认主题，仅注入动效样式
    │   └── styles/animations.css
    ├── client/              # 数据层：db / models / settings / backup / toast
    └── components/
        ├── display/         # 前台展示组件
        ├── admin/           # 管理后台组件
        └── ui/              # 通用 UI（弹窗 / 空状态 / Toast）
```

## 扩展新模块

1. 在 `docs/.vitepress/data/site-data.json` 增加集合字段。
2. 在 `client/models.js` 添加模型类（`add() / write() / del()`）。
3. 在 `components/display/` 新建展示组件、`components/admin/` 新建后台标签。
4. 新建页面 md，并在 `config.mts` 的 nav / sidebar 中登记。
