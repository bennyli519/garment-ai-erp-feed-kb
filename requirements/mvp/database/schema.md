# 数据库表结构设计

## 系统管理相关表

### 1. Company (公司表)
```prisma
model Company {
  id          String   @id @default(uuid())
  name        String   // 公司名称
  code        String   @unique  // 公司编码
  status      String   // 状态：active, inactive
  schemaName  String   @unique  // 对应的schema名称
  address     String?  // 公司地址
  contact     String?  // 联系人
  phone       String?  // 联系电话
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt

  // 关联
  users       User[]
  @@map("companies")
}
```

### 2. User (用户表)
```prisma
model User {
  id            String    @id @default(uuid())
  email         String    @unique
  password      String    // 加密存储
  name          String
  status        String    // active, inactive
  companyId     String
  departmentId  String?
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt

  // 关联
  company       Company   @relation(fields: [companyId], references: [id])
  department    Department? @relation(fields: [departmentId], references: [id])
  roles         UserRole[]
  @@map("users")
}
```

### 3. Role (角色表)
```prisma
model Role {
  id          String    @id @default(uuid())
  name        String
  code        String    @unique
  description String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  users       UserRole[]
  permissions RolePermission[]
  @@map("roles")
}

model UserRole {
  userId      String
  roleId      String
  createdAt   DateTime  @default(now())

  // 关联
  user        User      @relation(fields: [userId], references: [id])
  role        Role      @relation(fields: [roleId], references: [id])

  @@id([userId, roleId])
  @@map("user_role_assignments")
}
```

### 4. Permission (权限表)
```prisma
model Permission {
  id          String    @id @default(uuid())
  name        String
  code        String    @unique
  type        String    // menu, action, api
  description String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  roles       RolePermission[]
  @@map("permissions")
}

model RolePermission {
  roleId        String
  permissionId  String
  createdAt     DateTime  @default(now())

  // 关联
  role          Role        @relation(fields: [roleId], references: [id])
  permission    Permission  @relation(fields: [permissionId], references: [id])

  @@id([roleId, permissionId])
  @@map("role_permission_assignments")
}
```

## 组织架构相关表

### 5. Department (部门表)
```prisma
model Department {
  id          String    @id @default(uuid())
  name        String
  code        String    @unique
  parentId    String?
  path        String    // 存储部门层级路径
  level       Int       // 部门层级
  status      String    // active, inactive
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  parent      Department?  @relation("DepartmentTree", fields: [parentId], references: [id])
  children    Department[] @relation("DepartmentTree")
  employees   User[]
  @@map("departments")
}
```

### 6. Employee (员工表)
```prisma
model Employee {
  id            String    @id @default(uuid())
  code          String    @unique  // 工号
  name          String
  phone         String?
  email         String?
  position      String?   // 职位
  status        String    // active, inactive, resigned
  isActive      Boolean   @default(true)  // 是否在职
  birthDate     DateTime? // 出生日期
  hireDate      DateTime  // 入职日期
  resignDate    DateTime? // 离职日期
  departmentId  String
  userId        String?   // 关联用户ID（如果有系统账号）
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt

  // 关联
  department    Department @relation(fields: [departmentId], references: [id])
  user          User?      @relation(fields: [userId], references: [id])
  processes     EmployeeProcess[] // 关联工序
  @@map("employees")
}

model EmployeeProcess {
  id          String    @id @default(uuid())
  employeeId  String
  processId   String
  proficiency Int       @default(1)  // 熟练度等级
  isMain      Boolean   @default(false)  // 是否主要工序
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  employee    Employee  @relation(fields: [employeeId], references: [id])
  process     Process   @relation(fields: [processId], references: [id])

  @@unique([employeeId, processId])
  @@map("employee_process_assignments")
}
```

## 业务相关表

### 7. Process (工序表)
```prisma
model Process {
  id              String    @id @default(uuid())
  name            String    // 工序名称
  code            String    @unique  // 工序编号
  shortName       String    // 工序简称
  multiplier      Float     @default(1.0)  // 倍数
  basePrice       Float     // 原工价
  finalPrice      Float     // 最终工价（考虑倍数后）
  requirements    String?   // 工序要求
  qualityNotes    String?   // 质量说明
  categoryId      String    // 工序分类ID
  description     String?   // 描述
  standardTime    Float?    // 标准工时
  status          String    // active, inactive
  remark          String?   // 备注
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  // 关联
  category        ProcessCategory @relation(fields: [categoryId], references: [id])
  styleProcesses  ProductProcessAssignment[]
  employees       EmployeeProcess[]
  @@map("processes")
}

model ProcessCategory {
  id          String    @id @default(uuid())
  name        String
  code        String    @unique
  parentId    String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  parent      ProcessCategory?  @relation("CategoryTree", fields: [parentId], references: [id])
  children    ProcessCategory[] @relation("CategoryTree")
  processes   Process[]
  @@map("process_categories")
}
```

### 8. Product (款式表)
```prisma
model Product {
  id          String    @id @default(uuid())
  code        String    @unique  // 款号
  name        String    // 款式名称
  description String?   // 款式描述
  status      String    // draft, active, inactive
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  processes   ProductProcessAssignment[]
  sheets      ProcessSheet[]
  colors      ProductColorAssignment[]    // 关联颜色
  sizes       ProductSizeAssignment[]     // 关联尺码
  brands      ProductBrandAssignment[]    // 关联商标
  @@map("products")
}

model ProductProcessAssignment {
  id          String    @id @default(uuid())
  productId   String
  processId   String
  sequence    Int       // 工序顺序
  remark      String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  product     Product   @relation(fields: [productId], references: [id])
  process     Process   @relation(fields: [processId], references: [id])
  @@map("product_process_assignments")
}
```

### 9. Color (颜色表)
```prisma
model Color {
  id          String    @id @default(uuid())
  code        String    @unique  // 颜色编码
  name        String    // 颜色名称
  hexCode     String?   // 颜色十六进制码
  description String?   // 描述
  status      String    // active, inactive
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  products    ProductColorAssignment[]
  @@map("colors")
}

model ProductColorAssignment {
  id          String    @id @default(uuid())
  productId   String
  colorId     String
  isDefault   Boolean   @default(false)  // 是否默认颜色
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  product     Product   @relation(fields: [productId], references: [id])
  color       Color     @relation(fields: [colorId], references: [id])

  @@unique([productId, colorId])
  @@map("product_color_assignments")
}
```

### 10. Size (尺码表)
```prisma
model Size {
  id          String    @id @default(uuid())
  code        String    @unique  // 尺码编码
  name        String    // 尺码名称
  sizeType    String?   // 尺码类型：EU, US, UK等
  order       Int?      // 排序号
  description String?   // 描述
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  products    ProductSizeAssignment[]
  @@map("sizes")
}

model ProductSizeAssignment {
  id          String    @id @default(uuid())
  productId   String
  sizeId      String
  isDefault   Boolean   @default(false)  // 是否默认尺码
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  product     Product   @relation(fields: [productId], references: [id])
  size        Size      @relation(fields: [sizeId], references: [id])

  @@unique([productId, sizeId])
  @@map("product_size_assignments")
}
```

### 11. Brand (商标表)
```prisma
model Brand {
  id          String    @id @default(uuid())
  code        String    @unique  // 商标编码
  name        String    // 商标名称
  logo        String?   // 商标logo URL
  description String?   // 描述
  status      String    // active, inactive
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  products    ProductBrandAssignment[]
  @@map("brands")
}

model ProductBrandAssignment {
  id          String    @id @default(uuid())
  productId   String
  brandId     String
  position    String?   // 商标位置
  isMain      Boolean   @default(false)  // 是否主商标
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  product     Product   @relation(fields: [productId], references: [id])
  brand       Brand     @relation(fields: [brandId], references: [id])

  @@unique([productId, brandId])
  @@map("product_brand_assignments")
}
```

### 12. ProcessSheet (工艺单表)
```prisma
model ProcessSheet {
  id          String    @id @default(uuid())
  code        String    @unique  // 工艺单号
  productId   String    // 关联款式ID
  version     String    // 版本号
  status      String    // draft, pending, approved, rejected
  remark      String?
  createdBy   String
  approvedBy  String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt

  // 关联
  product     Product   @relation(fields: [productId], references: [id])
  creator     User      @relation("CreatedSheets", fields: [createdBy], references: [id])
  approver    User?     @relation("ApprovedSheets", fields: [approvedBy], references: [id])
  details     ProcessSheetDetail[]
  @@map("process_sheets")
}

model ProcessSheetDetail {
  id            String    @id @default(uuid())
  sheetId       String
  processId     String
  sequence      Int
  requirements  String?   // 工艺要求
  attachments   String?   // 附件链接（JSON数组）
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt

  // 关联
  sheet         ProcessSheet @relation(fields: [sheetId], references: [id])
  process       Process      @relation(fields: [processId], references: [id])
  @@map("process_sheet_details")
}
```

### 13. ProductionOrder (生产单表)
```prisma
model ProductionOrder {
  id              String    @id @default(uuid())
  code            String    @unique  // 生产单号
  productId       String    // 关联款式
  colorId         String    // 关联颜色
  sizeId          String    // 关联尺码
  quantity        Int       // 生产数量
  status          String    // draft, confirmed, in_production, completed, cancelled
  startDate       DateTime? // 开始日期
  endDate         DateTime? // 预计完成日期
  remark          String?   // 备注
  createdBy       String    // 创建人
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt

  // 关联
  product         Product   @relation(fields: [productId], references: [id])
  color           Color     @relation(fields: [colorId], references: [id])
  size            Size      @relation(fields: [sizeId], references: [id])
  creator         User      @relation(fields: [createdBy], references: [id])
  @@map("production_orders")
}
```

## 索引设计

### 性能索引
1. 用户表邮箱索引
```sql
CREATE INDEX idx_users_email ON users(email);
```

2. 部门树索引
```sql
CREATE INDEX idx_departments_path ON departments(path);
```

3. 工序编码索引
```sql
CREATE INDEX idx_processes_code ON processes(code);
```

4. 款式编码索引
```sql
CREATE INDEX idx_products_code ON products(code);
```

### 外键索引
**所有外键字段都会自动创建索引**

## Schema隔离设计

### 公共Schema (public)
- companies
- 系统级配置表

### 租户Schema (company_{id})
- 所有业务相关表
- 每个公司一个独立schema

## 审计日志
```prisma
model AuditLog {
  id          String    @id @default(uuid())
  userId      String
  action      String    // create, update, delete
  resource    String    // 资源类型
  resourceId  String    // 资源ID
  details     Json      // 变更详情
  createdAt   DateTime  @default(now())

  // 关联
  user        User      @relation(fields: [userId], references: [id])
  @@map("audit_logs")
}
``` 