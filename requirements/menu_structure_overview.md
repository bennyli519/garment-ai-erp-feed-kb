# Menu Structure Design

## Public Area (未登录区域)
- Home (首页)
- Pricing (价格方案)
- Features (功能介绍)
- Contact Us (联系我们)
- Login/Register (登录/注册)

## Platform Admin Dashboard (平台管理后台) 🏢
- Platform Overview (平台概览)
  - System Statistics (系统统计)
  - Active Companies (活跃企业)
  - Subscription Status (订阅状态)

- Company Management (企业管理)
  - Company List (企业列表)
  - Subscription Plans (订阅方案)
  - Company Approval (企业审核)

- Platform Settings (平台设置)
  - Global Settings (全局设置)
  - Email Templates (邮件模板)
  - System Maintenance (系统维护)
  - Security Controls (安全控制)

## Company Dashboard (企业后台) 💼

### System Management (系统管理) 🔧
- Employee Management (员工档案管理)
  - Employee Information (员工信息维护)
  - Employee Import (员工档案导入)
  - Employee Status (员工状态管理)
  - Department Management (部门管理)
    - Department Structure (部门结构设置)
    - Department Head Settings (部门主管设置)
    - Department Staff (部门人员管理)

- Permission Management (权限管理)
  - Role Management (角色管理)
  - Permission Settings (权限设置)
  - Operation Logs (操作日志)

### Basic Data (基础资料) 📊
- Basic Settings (基础设置)
  - Unit Management (单位管理)
    - Length Units (长度单位)
    - Weight Units (重量单位)
    - Package Units (包装单位)
  - Color Management (颜色管理)
    - Color Categories (颜色分类)
    - Color Codes (颜色编码)
  - Process Management (工序管理)
    - Process Categories (工序分类)
    - Process Definition (工序定义)
    - Process Price Settings (工序工价设置)
  - Size Management (尺码管理)
    - Size Group Settings (尺码组设置)
    - Size Specification (尺码规格定义)
  - Brand Management (商标管理)
    - Brand Information (商标信息)
    - Brand Images (商标图样)

### Production Management (生产管理) 🏭
- Style Management (款式管理)
  - Style Information (款式信息维护)
  - Style Images (款式图片管理)
  - Style Process Requirements (款式工艺要求)
  - Bill of Materials (款式物料清单)

- Process Sheet Management (工艺管理)
  - Process Sheet Generation (工艺单生成)
    - Process Configuration (工序配置)
    - Technical Requirements (工艺要求设置)
    - Technical Drawings (工艺图样上传)
  - Process Sheet List (工艺单列表)
    - Sheet Query (工艺单查询)
    - Sheet Approval (工艺单审核)
    - Sheet Printing (工艺单打印)

### Coming Soon Features (待实现功能) ⏳

- Inventory Management (库存管理)
  - Material Storage (物料入库)
  - Product Storage (成品入库)
  - Inventory Query (库存查询)
  - Stock Alert (库存预警)
  - Stock Taking (库存盘点)

- Salary Management (工资管理)
  - Work Ticket Management (工票管理)
    - Ticket Generation (工票生成)
    - Ticket Approval (工票审核)
    - Ticket Statistics (工票统计)
  - Piece Rate Salary (计件工资)
    - Salary Calculation (工资核算)
    - Salary Report (工资报表)

## Permission Settings (权限设置)

### Role Definitions (角色定义)
1. Company Administrator (企业管理员)
   - All feature permissions (所有功能的操作权限)
   - System settings permissions (系统设置权限)
   - Permission assignment rights (权限分配权限)

2. Department Head (部门主管)
   - Department staff management (本部门员工管理)
   - Department process management (本部门工艺管理)
   - Department ticket management (本部门工票管理)

3. Process Administrator (工艺管理员)
   - Style management permissions (款式管理权限)
   - Process sheet management permissions (工艺单管理权限)
   - Basic data view permissions (基础资料查看权限)

4. Regular Staff (普通员工)
   - Personal information view (个人信息查看)
   - Process sheet view (工艺单查看)
   - Work ticket view (工票查看)

## System Features (功能特点)

### Core Features (核心功能)
- Complete employee file management (完整的员工档案管理)
- Flexible process management (灵活的工序和工艺管理)
- Detailed style management system (详细的款式管理系统)
- Configurable basic data (可配置的基础资料)

### Extended Features (扩展功能)
- Salary calculation system (工资核算系统) [Coming Soon]
- Inventory management system (库存管理系统) [Coming Soon]
- Report statistics system (报表统计系统) [Coming Soon]

### System Characteristics (系统特性)
- Data import/export (数据导入导出)
- Batch operation support (批量操作支持)
- Operation log tracking (操作日志记录)
- Fine-grained permission control (权限精细控制)

## Access Control Matrix (访问控制矩阵)

### Platform Roles (平台角色)
1. Platform Admin (平台管理员)
   - Full platform access
   - Manage all companies
   - System configuration

2. Platform Operator (平台运营)
   - Company management
   - Basic platform operations
   - Support functions

### Company Roles (企业角色)
1. Company Admin (企业管理员)
   - Company-wide management
   - User management within company
   - Settings configuration

2. Department Manager (部门经理)
   - Department-level access
   - Team member management
   - Department data access

3. Regular User (普通用户)
   - Basic feature access
   - Personal data management
   - Assigned task management

## Menu Display Rules (菜单显示规则)

1. **Dynamic Menu Loading**
   - Based on user role
   - Based on permissions
   - Based on subscription level

2. **Menu State Management**
   - Remember last opened
   - Collapsible sections
   - Breadcrumb navigation

3. **Responsive Design**
   - Desktop view (完整菜单)
   - Tablet view (折叠菜单)
   - Mobile view (汉堡菜单)

## Future Module Placeholders (未来模块占位)

These modules will be grayed out or marked as "Coming Soon" in the MVP:

1. **Purchase Management** (采购管理)
   - Purchase Planning
   - Order Management
   - Supplier Management

2. **Inventory Management** (库存管理)
   - Stock Control
   - Warehouse Management
   - Inventory Tracking

3. **Financial Management** (财务管理)
   - Accounting
   - Billing
   - Financial Reports

4. **HR Management** (人力资源)
   - Employee Records
   - Attendance
   - Payroll

5. **Production Management** (生产管理)
   - Production Planning
   - Quality Control
   - Work Orders 