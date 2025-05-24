# Project Structure Design

## Monorepo Structure

```
garment-erp/
├── apps/
│   ├── admin/                  # 平台管理后台（包含API服务）
│   │   ├── app/               # Next.js App Router
│   │   │   ├── (auth)/       # 认证相关路由
│   │   │   ├── dashboard/    # 管理后台路由
│   │   │   └── api/         # API 路由（供 Portal 调用）
│   │   ├── components/       # 组件
│   │   ├── lib/             # 工具和服务
│   │   │   ├── auth/        # 认证相关
│   │   │   ├── db/          # 数据库操作
│   │   │   └── services/    # 业务服务
│   │   ├── prisma/          # 数据库配置
│   │   │   ├── schema.prisma
│   │   │   └── migrations/
│   │   ├── styles/          # 样式
│   │   └── package.json
│   │
│   └── portal/               # 企业门户（纯前端应用）
│       ├── app/              # Next.js App Router
│       │   ├── (auth)/      # 认证相关路由
│   │   └── dashboard/   # 企业后台路由
│   │   ├── components/      # 组件
│   │   ├── lib/            # 工具和服务
│   │   │   ├── api/        # API 客户端（调用 admin 的 API）
│   │   │   └── utils/      # 工具函数
│   │   ├── styles/         # 样式
│   │   └── package.json
│   │
│   └── .gitignore
│
└── turbo.json
```

## 系统架构

### Admin（管理后台）
- 完整的全栈应用
- 提供 API 服务
- 数据库操作和业务逻辑
- 系统管理功能

### Portal（企业门户）
- 纯前端应用
- 通过 API 调用 Admin 服务
- 专注于用户界面和交互
- 不直接操作数据库

## 技术栈

- Next.js 14 (App Router)
- TailwindCSS
- Prisma (仅 Admin)
- PostgreSQL (仅 Admin)
- TypeScript

## 开发环境

```bash
# 安装依赖
pnpm install

# 开发环境运行
pnpm dev

# 构建
pnpm build
```

## 技术栈详情

### 前端技术
- Next.js 14+ (App Router)
- TailwindCSS
- Shadcn/ui
- TypeScript
- React Query
- Zustand

### 后端技术 (集成在Next.js应用中)
- Next.js API Routes
- Prisma ORM
- PostgreSQL
- NextAuth.js

### 开发工具
- Turborepo
- ESLint
- Prettier
- Husky
- Jest
- Cypress

## 开发环境设置

### 必要条件
- Node.js 18+
- pnpm 8+
- Docker
- PostgreSQL 15+

### 开发命令
```bash
# 安装依赖
pnpm install

# 开发环境运行
pnpm dev

# 构建
pnpm build

# 测试
pnpm test

# 代码检查
pnpm lint
```

## 部署架构

### 开发环境
- Vercel (前端应用)
- AWS RDS (PostgreSQL)
- AWS S3 (文件存储)

### 生产环境
- 负载均衡
- 多区域部署
- 数据库主从复制
- CDN 分发

## 安全考虑

### 数据隔离
- 租户级别的数据隔离
- Schema级别的权限控制
- 行级别的访问控制

### 认证授权
- JWT认证
- RBAC权限控制
- API访问控制

### 数据安全
- 数据加密存储
- 传输加密 (HTTPS)
- 审计日志

## CI/CD流程

### 开发流程
1. 功能分支开发
2. 代码审查
3. 自动化测试
4. 预览环境部署
5. 生产环境部署

### 自动化测试
- 单元测试
- 集成测试
- E2E测试
- 性能测试

<!-- ### 监控告警
- 错误追踪
- 性能监控
- 用户行为分析
- 系统健康检查  -->