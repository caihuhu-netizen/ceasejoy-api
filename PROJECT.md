# PROJECT.md - GAMEHOT CDP 游戏增长系统重构

## 项目概述
面向休闲游戏发行团队的全栈产品优化平台（CDP - Customer Data Platform）
核心方法论：**获取用户 → 理解用户 → 分层运营 → 精准触达 → 变现优化 → 效果验证**

## 原始技术栈（Manus）
- 前端：React 19 + Tailwind CSS 4
- 后端：Express 4 + tRPC 11 + Drizzle ORM
- 数据库：MySQL / TiDB
- 规模：55个Router、55个DB模块、109张表、57个前端页面

## 重构技术栈
- 前端：**保留原版 React 19 + Tailwind CSS 4**（只改API调用方式）
- 后端：**Spring Boot 3.2 + Java 21**
- ORM：Spring Data JPA + MyBatis（复杂查询）
- 数据库：MySQL 8.0（已部署）
- 缓存：Redis（已部署）
- 消息队列：RabbitMQ（已部署）
- 搜索：Elasticsearch（已部署）
- 文件存储：MinIO（已部署）
- 部署：Docker + GitHub Actions CI/CD → 阿里云ECS

## 五大业务域（57个页面）

### 1. 产品优化（7个模块）
- 经营仪表盘 `/`
- AI 日报 `/daily-report`
- 版本管理 `/version-management`
- 优化建议 `/optimization-suggestions`
- 效果验证 `/effect-verification`
- A/B 实验 `/experiments`
- 对比分析 `/comparison-analysis`

### 2. 用户洞察（8个模块）
- 用户分层 `/segments`
- 用户画像 `/user-profiles`
- 用户分群 `/audience`
- 分群模板库 `/audience/templates`
- Cohort留存 `/cohort-retention`
- 闭环引擎 `/loop-engine`
- 事件分析 `/event-analysis`
- 数据分析 `/analytics`

### 3. 经营数据（11个模块）
- 每日总览 `/daily-overview`
- 投放管理 `/acquisition`
- 变现管理 `/monetize`
- 广告聚合 `/ad-revenue`
- 内购商品 `/iap-products`
- 智能定价 `/pricing-engine`
- 成本利润 `/cost-profit`
- 异常监控 `/anomaly-monitor`
- 运营工具箱 `/ops-tools`
- 自定义报表 `/custom-report`
- 数据导出 `/data-export`

### 4. 游戏配置（7个模块）
- 关卡管理 `/levels`
- 探针关卡 `/probes`
- 难度调度 `/difficulty`
- 用户召回 `/user-recall`
- 推送中心 `/push-center`
- 配置版本 `/config-versions`
- 系统配置 `/config`

### 5. 系统与运营（待补充）

## 重构策略

### 阶段一：核心基础（优先）
1. 用户认证（登录/权限/飞书OAuth）
2. 游戏项目管理（多游戏支持）
3. 经营仪表盘（KPI数据展示）
4. 数据库表结构迁移

### 阶段二：用户数据
5. 用户分层引擎
6. 用户画像
7. 分群条件引擎
8. 事件分析

### 阶段三：经营数据
9. 每日数据汇总
10. AppsFlyer数据同步
11. 广告收入聚合
12. 内购商品管理

### 阶段四：智能功能
13. A/B实验系统
14. 闭环引擎（自动化运营）
15. AI日报（LLM集成）
16. 智能定价引擎

### 阶段五：游戏配置
17. 关卡管理
18. 难度调度
19. 推送中心
20. 配置版本管理

## 微服务拆分规划（长期）
```
gateway-service     # API网关（Nginx + Spring Cloud Gateway）
auth-service        # 认证授权
analytics-service   # 数据分析引擎
config-service      # 游戏配置管理
push-service        # 推送中心
ai-service          # AI/LLM功能
```

## 关键外部集成
- AppsFlyer（投放数据同步）
- 飞书OAuth（企业登录）
- AppLovin/广告网络（广告收入）
- LLM（AI日报/优化建议）

## 项目路径
- 源码（Manus）：/home/mulerun/.openclaw/workspace/game-growth-system
- 重构后端：/home/mulerun/.openclaw/workspace/ceasejoy-api
- GitHub：https://github.com/caihuhu-netizen/ceasejoy-api
