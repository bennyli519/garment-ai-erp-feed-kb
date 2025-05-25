# Menu Structure Design (MVP Version)

## Public Area (未登录区域)
- Home (首页)
- Login/Register (登录/注册)

## Platform Admin Dashboard (平台管理后台) 🏢
- Platform Overview (平台概览)
  - System Statistics (系统统计)
  - Active Companies (活跃企业)

- Company Management (企业管理)
  - Company List (企业列表)
  - Company Approval (企业审核)

## Company Dashboard (企业后台) 💼

### System Management (系统管理) 🔧
- Employee Management (员工档案管理)
  - Employee Information (员工信息维护)
  - Department Management (部门管理)
    - Department Structure (部门结构设置)
    - Department Staff (部门人员管理)

- Permission Management (权限管理)
  - Role Management (角色管理)
  - Permission Settings (权限设置)

### Basic Data (基础资料) 📊
- Basic Settings (基础设置)
  - Process Management (工序管理)
    - Process Categories (工序分类)
    - Process Definition (工序定义)
    - Process Price Settings (工序工价设置)
  - Size Management (尺码管理)
    - Size Group Settings (尺码组设置)
    - Size Specification (尺码规格定义)

### Production Management (生产管理) 🏭
- Style Management (款式管理)
  - Style Information (款式信息维护)
  - Style Process Requirements (款式工艺要求)

- Process Sheet Management (工艺管理)
  - Process Sheet Generation (工艺单生成)
    - Process Configuration (工序配置)
    - Technical Requirements (工艺要求设置)
  - Process Sheet List (工艺单列表)
    - Sheet Query (工艺单查询)
    - Sheet Approval (工艺单审核)

## Permission Settings (权限设置)

### Role Definitions (角色定义)
1. Company Administrator (企业管理员)
   - All feature permissions (所有功能的操作权限)
   - System settings permissions (系统设置权限)

2. Department Head (部门主管)
   - Department staff management (本部门员工管理)
   - Process sheet management (工艺单管理)

3. Regular Staff (普通员工)
   - Personal information view (个人信息查看)
   - Process sheet view (工艺单查看)

## System Features (功能特点)

### Core Features (核心功能)
- Basic employee management (基础员工管理)
- Process sheet workflow (工艺单流程)
- Style management (款式管理)
- Department management (部门管理)

### System Characteristics (系统特性)
- Role-based access control (基于角色的访问控制)
- Process sheet approval flow (工艺单审批流程)
- Basic data management (基础资料管理) 