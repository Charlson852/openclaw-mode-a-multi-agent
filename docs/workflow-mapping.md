# 当前工作流映射（Mode A）

## 一、A股中台链

### 默认角色分工
- `analyst`：主执行
- `reviewer`：结果复核（仅中台日报链）
- `monitor`：发送与产物巡检
- `main`：汇总与对用户回复

### 当前关键任务
- `A-share limit-up review`
- `A-share review reviewer-check`
- `A-share limit-up review resend check`
- `ops monitor patrol`（同时巡中台与博客落地）

### 当前状态
- 已真实跑通 build → deep analysis → send → sent 标记写入
- reviewer 已收敛为只审 A 股中台链，不再误审博客

---

## 二、博客发布链

### 默认角色分工
- `publisher`：主执行
- `reviewer`：博客审核
- `monitor`：文件/状态巡检
- `main`：汇总与对用户回复

### 当前关键任务
- `daily-blog-post`
- `blog reviewer-check`
- `ops monitor patrol`

### 当前状态
- 已真实跑通：生成文章 → git commit → git push → 用户通知
- 曾发生一次“错误执行上下文”事故，现已修正 cron 提示词与模型口径
- 仍建议后续继续加强 reviewer / monitor 与主链结果对齐

---

## 三、ops 运维链

### 默认角色分工
- `ops`：主执行
- `reviewer`：修复结果复检
- `monitor`：巡检 / 告警
- `main`：汇总与对用户回复

### 当前关键任务
- `sync-mode-a-repo`
- `auto-sync-models`
- `ops recovery reviewer-check`
- `ops monitor patrol`

### 当前状态
- 仓库同步、模型自动清理已开始按 ops 口径执行
- 运维修复复检、巡检任务已完成命名和口径收敛
- 宝塔 / 反代 / 网关 / 配置类任务已归入 ops 默认职责

---

## 四、当前未完全自动化的部分

### 1. 临时人工任务
- 主对话中临时发起的任务，仍有一部分由 `main` 直接执行
- 后续应继续把这部分默认路由固化

### 2. reviewer / monitor 收尾一致性
- 已经修过一轮误报
- 但仍建议继续观察几天，确保复核链与主链完全一致

### 3. skills / 权限硬隔离
- 当前仍是软分工
- 后续再推进严格技能白名单和更细权限矩阵
