# 中医药科普平台 - B端管理网站

一个基于 Vue 3 + Element Plus 的中医药科普网站管理端，提供中药材、药膳配方、常见病症等内容的管理和展示功能。

## 技术栈

- **Vue 3** - 渐进式 JavaScript 框架
- **TypeScript** - 类型安全的 JavaScript
- **Vite** - 下一代前端构建工具
- **Vue Router** - 官方路由管理器
- **Pinia** - 新一代状态管理库
- **Element Plus** - 基于 Vue 3 的组件库
- **Axios** - HTTP 客户端

## 功能特性

### 页面与路由
- ✅ 首页 - 数据概览和热门内容推荐
- ✅ 中医药材库 - 药材列表和详情页
- ✅ 药膳配方 - 配方列表和详情页
- ✅ 常见病症 - 病症列表和详情页
- ✅ 内容分类浏览页
- ✅ 内容详情页

### 核心组件
- ✅ **ContentCard** - 通用内容卡片组件，支持图片、标题、描述展示和收藏功能
- ✅ **CommentSection** - 评论组件，集成发表和展示评论功能
- ✅ **CategoryFilter** - 分类筛选组件，支持多维度筛选

### 数据交互
- ✅ Axios 封装，统一 API 请求处理
- ✅ Pinia 状态管理，管理用户信息和收藏列表
- ✅ RESTful API 集成

### 用户体验
- ✅ 响应式设计，支持移动端和桌面端
- ✅ Element Plus Loading 加载动画
- ✅ 多维度分类浏览和搜索功能
- ✅ 收藏功能
- ✅ 评论功能

## 快速开始

### 安装依赖

使用 yarn（推荐）：
```bash
yarn install
```

或使用 npm：
```bash
npm install
```

### 开发模式

使用 yarn：
```bash
yarn serve
# 或
yarn dev
```

使用 npm：
```bash
npm run dev
```

项目将在 `http://localhost:3000` 启动

### 构建生产版本

```bash
yarn build
# 或
npm run build
```

### 预览生产构建

```bash
yarn preview
# 或
npm run preview
```

## 项目结构

```
.
├── src/
│   ├── api/              # API 接口定义
│   │   ├── request.ts    # Axios 封装
│   │   ├── herbs.ts      # 药材相关 API
│   │   ├── recipes.ts    # 药膳相关 API
│   │   ├── diseases.ts   # 病症相关 API
│   │   └── comments.ts   # 评论相关 API
│   ├── components/       # 公共组件
│   │   ├── ContentCard.vue        # 内容卡片组件
│   │   ├── CommentSection.vue     # 评论组件
│   │   └── CategoryFilter.vue     # 筛选组件
│   ├── layouts/          # 布局组件
│   │   └── MainLayout.vue # 主布局
│   ├── router/           # 路由配置
│   │   └── index.ts
│   ├── stores/           # Pinia 状态管理
│   │   └── user.ts       # 用户状态
│   ├── views/            # 页面组件
│   │   ├── HomeView.vue           # 首页
│   │   ├── HerbsView.vue          # 药材列表
│   │   ├── HerbDetailView.vue     # 药材详情
│   │   ├── RecipesView.vue        # 配方列表
│   │   ├── RecipeDetailView.vue   # 配方详情
│   │   ├── DiseasesView.vue       # 病症列表
│   │   ├── DiseaseDetailView.vue  # 病症详情
│   │   └── CategoryView.vue       # 分类浏览
│   ├── App.vue           # 根组件
│   └── main.ts           # 入口文件
├── index.html            # HTML 模板
├── vite.config.ts        # Vite 配置
├── tsconfig.json         # TypeScript 配置
└── package.json          # 项目配置
```

## 环境配置

创建 `.env` 文件（参考 `.env.example`）：

```env
VITE_API_BASE_URL=http://localhost:8080/api
```

## API 接口说明

项目已配置好 API 接口结构，需要后端 Spring Boot 提供以下接口：

### 药材相关
- `GET /api/herbs` - 获取药材列表
- `GET /api/herbs/:id` - 获取药材详情
- `POST /api/herbs/:id/favorite` - 收藏药材
- `DELETE /api/herbs/:id/favorite` - 取消收藏

### 药膳相关
- `GET /api/recipes` - 获取配方列表
- `GET /api/recipes/:id` - 获取配方详情
- `POST /api/recipes/:id/favorite` - 收藏配方
- `DELETE /api/recipes/:id/favorite` - 取消收藏

### 病症相关
- `GET /api/diseases` - 获取病症列表
- `GET /api/diseases/:id` - 获取病症详情
- `POST /api/diseases/:id/favorite` - 收藏病症
- `DELETE /api/diseases/:id/favorite` - 取消收藏

### 评论相关
- `GET /api/comments` - 获取评论列表
- `POST /api/comments` - 发表评论
- `DELETE /api/comments/:id` - 删除评论

## 开发指南

1. **添加新页面**：在 `src/views/` 目录下创建 Vue 组件，并在 `src/router/index.ts` 中添加路由配置

2. **添加新组件**：在 `src/components/` 目录下创建组件，使用 `<script setup>` 语法

3. **添加 API 接口**：在 `src/api/` 目录下创建对应的 API 文件，使用统一的 `request` 实例

4. **状态管理**：在 `src/stores/` 目录下创建 Pinia store

5. **样式规范**：使用 Element Plus 组件和样式，自定义样式使用 scoped

## 浏览器支持

现代浏览器和 IE11（需要 polyfill）

## License

MIT
