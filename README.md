# 意象客户关系管理系统（yshop-crm）

一个前后端分离的企业级客户关系管理系统（CRM），覆盖客户全生命周期管理：线索 → 商机 → 客户 → 合同 → 回款，并内置销售数据分析看板。

基于 [yshop-crm](https://gitee.com/guchengwuyue/crm) 开源项目二次开发，本地化部署可用。

## 技术栈

| 端 | 技术 |
|---|---|
| 后端 | Spring Boot 3.2 / MyBatis-Plus / Spring Security OAuth2 / JWT / Redis / MySQL 8 |
| 前端 | Vue 3 / Vite 5 / Element Plus / TypeScript |
| 其他 | Maven 多模块、Knife4j 接口文档、Quartz 定时任务 |

## 核心功能

- **客户管理**：客户列表、客户跟踪、联系人、公海、客户查重、客户领取、批量导入、转移客户
- **商机管理**：商机需求、跟进记录、产品关联
- **线索管理**：线索列表、跟进、线索池、转客、批量导入
- **合同管理**：合同录入、审核流、收款回款、合同打印
- **发票管理**：发票开具、审核
- **数据分析**：员工业绩、客户级别、客户行业、合同排行
- **系统管理**：用户/角色/菜单权限（RBAC）、操作日志

## 项目结构

```
├── yshop-crm/          # 后端（Maven 多模块）
│   ├── yshop-server/   # 启动模块（端口 48081）
│   ├── yshop-module-crm/    # CRM 业务模块
│   ├── yshop-module-system/ # 系统/权限模块
│   ├── yshop-module-mall/   # 商城模块
│   └── sql/            # 数据库脚本（含完整初始化数据）
└── yshop-crm-vue/      # 前端（Vue3 + Vite，端口 80）
```

## 本地快速启动

### 环境要求
- JDK 17、Maven 3.8+
- MySQL 8.0、Redis 6+
- Node.js 16+、pnpm / npm

### 步骤

```bash
# 1. 初始化数据库（默认库名 yshop-crm-open-source）
mysql -uroot -p < yshop-crm/sql/yshop-crm-open-source.sql

# 2. 启动 Redis
redis-server

# 3. 启动后端（默认端口 48081）
cd yshop-crm
mvn clean install -Dmaven.test.skip=true
java -jar yshop-server/target/yshop-server.jar

# 4. 启动前端（默认端口 80）
cd yshop-crm-vue
npm install --legacy-peer-deps
npm run dev
```

> 数据库账号默认 `root/root`，Redis 默认 `127.0.0.1:6379`，
> 如需修改请编辑 `yshop-crm/yshop-server/src/main/resources/application-local.yaml`。

### 登录账号
- 管理员：`admin / admin123`
- 接口文档：http://localhost:48081/swagger-ui
- 前端地址：http://localhost:80

## 二次开发说明

本项目在开源版基础上做了以下本地化适配：
- element-plus 升级至 2.14.x，修复 `@form-create` 组件依赖缺失导致前端无法启动的问题
- 关闭登录页验证码，便于本地联调
- 补充 `pnpm-workspace.yaml` 以兼容新版 pnpm

## License

MIT
