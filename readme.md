# 云笔记 (CF Note)

基于 Cloudflare Workers + D1 数据库的轻量云笔记应用，前端使用纯 HTML + 原生 JS。

## 项目结构

```
cf_note/
├── wrangler.toml      # Workers 配置 + D1 数据库绑定
├── schema.sql         # 建表语句 + 预置 admin 用户
├── src/
│   └── index.js       # Worker 后端（API 路由 + 静态页面服务）
└── index.html         # 前端页面（HTML + 原生 JS）
```

## 功能

- 笔记的增删改查
- 用户列表展示
- 预置 admin 用户（admin/admin123）

## API

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/` | 返回前端页面 |
| GET | `/api/users` | 获取用户列表 |
| GET | `/api/notes` | 获取笔记列表 |
| POST | `/api/notes` | 创建笔记 |
| PUT | `/api/notes/:id` | 更新笔记 |
| DELETE | `/api/notes/:id` | 删除笔记 |

## 快速开始

### 1. 安装 Wrangler

```bash
npm install -g wrangler
```

### 2. 创建 D1 数据库

```bash
wrangler d1 create cf-note-db
```

将返回的 `database_id` 替换到 `wrangler.toml` 中。

### 3. 初始化数据库

```bash
wrangler d1 execute cf-note-db --local --file=schema.sql
```

### 4. 本地开发

```bash
wrangler dev
```

浏览器访问 `http://localhost:8787`。

### 5. 部署到 Cloudflare

```bash
# 先初始化远程数据库
wrangler d1 execute cf-note-db --remote --file=schema.sql

# 部署 Worker
wrangler deploy
```

## 技术栈

- **后端**: Cloudflare Workers
- **数据库**: Cloudflare D1 (SQLite)
- **前端**: HTML + 原生 JavaScript (Fetch API)
