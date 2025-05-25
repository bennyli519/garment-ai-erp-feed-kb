# Project Structure Design

## Application Structure

```
garment-erp/
├── src/
│   ├── client/                    # 前端相关的所有内容
│   │   ├── components/           # UI组件
│   │   │   ├── admin/           # 管理后台组件
│   │   │   │   ├── layout/      # 布局组件
│   │   │   │   ├── features/    # 功能组件
│   │   │   │   └── ui/          # 基础UI组件
│   │   │   └── shared/          # 共享组件（为门户预留）
│   │   │
│   │   ├── hooks/               # React Hooks
│   │   │   ├── admin/          
│   │   │   └── shared/         
│   │   │
│   │   ├── stores/              # 状态管理
│   │   │   ├── admin/          
│   │   │   └── shared/         
│   │   │
│   │   ├── styles/              # 样式文件
│   │   │   ├── admin/
│   │   │   └── shared/
│   │   │
│   │   └── utils/               # 前端工具函数
│   │
│   ├── core/                     # 核心业务逻辑
│   │   ├── use-cases/           # 业务用例
│   │   │   ├── admin/          # 管理后台用例
│   │   │   └── shared/         # 共享用例
│   │   └── services/            # 核心服务
│   │
│   ├── domain/                   # 领域层
│   │   ├── tenant/             
│   │   ├── user/               
│   │   ├── procurement/        
│   │   ├── inventory/          
│   │   └── shared/            
│   │
│   ├── infrastructure/          # 基础设施层
│   │   ├── database/          
│   │   │   ├── prisma/        
│   │   │   └── repositories/   
│   │   ├── auth/              
│   │   └── services/          
│   │
│   └── app/                     # Next.js App Router
│       ├── admin/              # 管理后台路由 (/admin/*)
│       │   ├── layout.tsx
│       │   ├── dashboard/
│       │   ├── tenants/
│       │   └── settings/
│       ├── api/                # API 路由
│       │   ├── admin/         # 管理后台 API
│       │   └── shared/        # 共享 API
│       └── (portal)/          # 预留门户路由（暂不实现）
│
├── public/                     # 静态资源
│   ├── admin/                 
│   └── shared/               
│
├── prisma/                    # Prisma 配置和迁移
│   ├── schema.prisma
│   └── migrations/
│
├── types/                     # 类型定义
├── tests/                     # 测试文件
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── .env.example              
├── package.json
└── tsconfig.json
```

## 技术栈

### 核心技术
- Next.js 14+ (App Router)
- TypeScript
- TailwindCSS
- Shadcn/ui
- Prisma ORM
- PostgreSQL

### 状态管理
- React Query (TanStack Query)
- Zustand

### 开发工具
- ESLint
- Prettier
- Husky
- Jest
- Cypress

## 开发环境设置

### 必要条件
- Node.js 18+
- pnpm 8+
- PostgreSQL 15+
- Docker (可选，用于数据库)

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
- Vercel (应用部署)
- AWS RDS (PostgreSQL)
- AWS S3 (文件存储)

## 安全考虑

### 数据隔离
- 租户级别的数据隔离
- Schema级别的权限控制
- 行级别的访问控制

### 认证授权
- NextAuth.js
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
- 单元测试 (Jest)
- 集成测试
- E2E测试 (Cypress)
- 性能测试

### 监控告警
- Sentry 错误追踪
- Vercel Analytics
- 系统健康检查