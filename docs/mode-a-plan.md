# Mode A 第一版实施方案

## 定义

Mode A = **单入口、多执行者**。

- 用户只与 `main` 对话
- `main` 判断任务类型
- 将任务派给常驻专职 Agent
- 再统一汇总结果回复用户

## 第一版目标

先实现 3 个常驻 Agent：
- `analyst`
- `publisher`
- `ops`

## 为什么先做 3 个

因为第一版追求的是：
- 能跑
- 稳定
- 好维护
- 不打断现有使用习惯

## 角色说明

### analyst
负责研究底稿：
- A股盘面
- 板块强弱
- 个股研究
- 商品 / 期货 / 宏观

### publisher
负责发布交付：
- 博客文章
- frontmatter
- Git push
- Cloudflare Pages 构建
- 复盘发送链路

### ops
负责稳定性：
- 网关 / 配置 / cron / hook
- Docker / Nginx / 宝塔 / 反代
- 服务器排障

## 工作流

### 分析链
用户 -> main -> analyst -> main -> 用户

### 发布链
用户 -> main -> analyst（可选）-> publisher -> main -> 用户

### 运维链
用户 -> main -> ops -> main -> 用户

## 第一版不做

- 不上 reviewer
- 不上 12 个 full 三省六部角色
- 不做 Telegram 直接进看板下旨
- 不做复杂权限矩阵
- 不做严格 skills 白名单

## 第二阶段再做

- reviewer 审核官
- 硬隔离 skills
- 更细的 Agent 权限矩阵
- 看板驱动调度
