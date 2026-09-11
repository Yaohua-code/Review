# Web 复习刷题库

一个纯前端在线刷题网站，聚合 **Web 前端 / Python / 互联网前沿新技术** 三大题库共 **1069 道题**，覆盖单选、填空、判断、简答、综合 5 种题型。主打"筛选 → 作答 → 即时反馈 → 错题强化"的复习闭环，零部署成本、即开即用。

🔗 在线体验：<https://yaohua-code.github.io/Review/>

## 功能特性

- **多题库切换**：Web 前端（358 题）、Python（335 题）、互联网前沿新技术（376 题）
- **双重筛选**：按题型 + 章节自由组合，精准定位练习范围
- **即时判分**：单选/判断点击即判并高亮正确答案；填空自动忽略大小写与空白差异
- **进度持久化**：答题记录存于 `localStorage`，刷新不丢失
- **错题本**：自动收集错题，答对后自动移出，支持反复强化
- **看题模式**：只读浏览题干与答案，适合考前速览
- **统计看板**：已答 / 答对 / 答错 / 正确率实时统计
- **选题面板**：按题号快速跳转，绿/红标记答题状态
- **暗色主题**：跟随系统偏好，可手动切换

## 技术栈

| 维度 | 选型 |
|------|------|
| 框架 | Vue 3（Composition API + `<script setup>`） |
| 语言 | TypeScript（可辨识联合建模题目类型） |
| 构建 | Vite |
| 测试 | Vitest + @vue/test-utils + happy-dom |
| 数据 | 打包 JSON（`src/data/questions.json`），由 Node 脚本从 docx / xlsx / py 自动生成 |

## 快速开始

```bash
# 安装依赖
npm install

# 本地开发
npm run dev

# 类型检查 + 构建
npm run build

# 本地预览构建产物
npm run preview

# 运行测试
npm run test

# 重新生成题库数据（解析 docx / xlsx / py 源文件 → questions.json）
node scripts/build-questions.mjs
```

## 项目结构

```
├── index.html
├── vite.config.ts              # Vite + Vitest 配置
├── scripts/
│   └── build-questions.mjs     # 多格式题库解析脚本（docx / xlsx / py → JSON）
├── public/                     # 静态资源
├── questionBank/               # 题库源文件（docx / xlsx / py / doc）
├── docs/                       # 产品设计文档、技术方案
└── src/
    ├── main.ts
    ├── App.vue                 # 主界面编排（筛选 / 导航 / 统计 / 错题本）
    ├── style.css               # 全局样式与主题变量
    ├── types.ts                # 题型可辨识联合类型
    ├── data/
    │   ├── questions.json      # 结构化题库（脚本生成物）
    │   └── raw/                # 中间数据源
    ├── lib/
    │   ├── questions.ts        # 筛选 / 判分 / 章节工具（纯函数）
    │   └── progress.ts         # 进度存储（localStorage 封装）
    └── components/
        └── QuestionCard.vue    # 题目卡片 + 即时判分交互
```

## 测试

共 **44 个用例**（4 个测试文件），覆盖：

- 判分逻辑：单选 / 判断 / 填空（大小写、空白容错）
- 筛选逻辑：题型 / 章节过滤、章节去重保序
- 进度存储：读写、统计、覆盖、重置
- 组件交互：即时判分、填空核对、单题只答一次
- 主界面：题库切换、筛选联动、错题本模式

## 部署

项目采用 `gh-pages` 分支部署到 GitHub Pages：

```bash
npm run deploy   # 构建 dist 并推送到 gh-pages 分支
```

部署前需在仓库 Settings → Pages 中将 Source 指向 **`gh-pages` 分支 / 根目录**（`vite.config.ts` 已配置 `base: './'` 相对路径，适配子路径访问）。

## 文档

- [产品设计文档](./docs/产品设计文档.md)
- [技术方案](./docs/技术方案.md)
