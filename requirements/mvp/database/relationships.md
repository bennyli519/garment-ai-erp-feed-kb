# 数据库关系设计

## 系统管理关系

### 公司-用户关系
- Company (1) ←→ User (*)
  - 一个公司可以有多个用户
  - 每个用户必须属于一个公司
  - 通过 `companyId` 外键关联

### 用户-角色-权限关系
- User (*) ←→ Role (*) [通过 UserRoleAssignment]
  - 多对多关系
  - 一个用户可以有多个角色
  - 一个角色可以分配给多个用户

- Role (*) ←→ Permission (*) [通过 RolePermissionAssignment]
  - 多对多关系
  - 一个角色可以有多个权限
  - 一个权限可以属于多个角色

## 组织架构关系

### 部门关系
- Department (1) ←→ Department (*) [自引用]
  - 树形结构
  - 一个部门可以有多个子部门
  - 每个部门最多有一个父部门
  - 通过 `parentId` 和 `path` 维护层级

### 部门-员工关系
- Department (1) ←→ Employee (*)
  - 一个部门可以有多个员工
  - 每个员工必须属于一个部门
  - 通过 `departmentId` 外键关联

### 员工-用户关系
- Employee (1) ←→ User (0..1)
  - 一个员工可以有一个系统用户账号（可选）
  - 一个用户账号对应一个员工
  - 通过 `userId` 外键关联

### 员工-工序关系
- Employee (*) ←→ Process (*) [通过 EmployeeProcessAssignment]
  - 多对多关系
  - 一个员工可以负责多个工序
  - 一个工序可以由多个员工负责
  - 包含熟练度和是否主要工序信息

## 业务关系

### 工序分类关系
- ProcessCategory (1) ←→ ProcessCategory (*) [自引用]
  - 树形结构
  - 一个分类可以有多个子分类
  - 每个分类最多有一个父分类
  - 通过 `parentId` 关联

### 工序-分类关系
- ProcessCategory (1) ←→ Process (*)
  - 一个分类可以包含多个工序
  - 每个工序必须属于一个分类
  - 通过 `categoryId` 外键关联

### 款式相关关系
- Product (*) ←→ Process (*) [通过 ProductProcessAssignment]
  - 多对多关系
  - 一个款式可以包含多个工序
  - 一个工序可以用于多个款式
  - 包含顺序信息

- Product (*) ←→ Color (*) [通过 ProductColorAssignment]
  - 多对多关系
  - 一个款式可以有多个颜色
  - 一个颜色可以用于多个款式

- Product (*) ←→ Size (*) [通过 ProductSizeAssignment]
  - 多对多关系
  - 一个款式可以有多个尺码
  - 一个尺码可以用于多个款式

- Product (*) ←→ Brand (*) [通过 ProductBrandAssignment]
  - 多对多关系
  - 一个款式可以有多个商标
  - 一个商标可以用于多个款式
  - 包含商标位置信息

### 工艺单关系
- Product (1) ←→ ProcessSheet (*)
  - 一个款式可以有多个工艺单
  - 每个工艺单必须对应一个款式
  - 通过 `productId` 外键关联

- ProcessSheet (1) ←→ ProcessSheetDetail (*)
  - 一个工艺单包含多个工序明细
  - 每个明细必须属于一个工艺单
  - 通过 `sheetId` 外键关联

### 生产单关系
- Product (1) ←→ ProductionOrder (*)
  - 一个款式可以有多个生产单
  - 每个生产单必须对应一个款式
  - 通过 `productId` 外键关联

- ProductionOrder (1) ←→ Color (1)
  - 每个生产单对应一个颜色
  - 通过 `colorId` 外键关联

- ProductionOrder (1) ←→ Size (1)
  - 每个生产单对应一个尺码
  - 通过 `sizeId` 外键关联

## 审计关系

### 操作审计
- User (1) ←→ AuditLog (*)
  - 记录用户所有关键操作
  - 包含操作类型、资源信息
  - 通过 `userId` 外键关联

## 数据完整性

### 级联删除规则
1. 公司删除时：
   - 关联用户设置为无效
   - 保留历史数据

2. 部门删除时：
   - 检查是否有子部门
   - 检查是否有员工
   - 禁止删除非空部门

3. 工序分类删除时：
   - 检查是否有子分类
   - 检查是否有关联工序
   - 禁止删除非空分类

4. 款式删除时：
   - 检查是否有关联的生产单
   - 检查是否有关联的工艺单
   - 禁止删除有关联数据的款式

### 数据验证规则
1. 用户邮箱唯一性
2. 编码字段唯一性（公司编码、员工工号、款号等）
3. 状态字段枚举值验证
4. 必填字段非空验证 