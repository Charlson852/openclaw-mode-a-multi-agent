# OpenClaw Mode A Multi-Agent

> **一个适合个人助手场景的轻量多 Agent 协作方案**  
> 你只和主 Agent 对话，主 Agent 在后台调度多个常驻专职 Agent 完成分析、发布、运维等任务。

---

## 为什么要做这个项目？

大多数多 Agent 框架的问题不是“能力不够强”，而是：

- 用户必须自己挑 Agent
- 任务一复杂就容易失控
- 结果不可观测、不可追责
- 一旦把所有事情都交给一个 Agent，系统会越来越重、越来越乱

**Mode A** 的目标就是解决这个问题：

> **保留“只跟一个助手说话”的体验，同时在后台实现专职分工。**

它不是一个炫技型多 Agent 项目，而是一套**面向真实日常使用**的协作模式。

---

## 一句话说明 Mode A

Mode A = **单入口，多执行者**。

也就是：

- 用户只和 `main` 对话
- `main` 判断任务类型
- `main` 把任务交给合适的常驻 Agent
- 子 Agent 完成后，把结果回传给 `main`
- `main` 再统一整理后回复用户

用户永远不需要直接跟 analyst / publisher / ops 对话。

---

## 适合什么场景？

这个方案尤其适合下面这类个人助手工作流：

- **A股复盘与盘后发布**
- **博客自动发布 / GitHub 推送 / Pages 构建检查**
- **OpenClaw / Docker / 服务器 / 反代排障**
- **研究、发布、运维并行进行，但又不想自己切换多个 Agent**

如果你经常遇到：
- 一个 Agent 同时分析盘面、修服务器、发博客
- 任务越来越杂，提示词越来越臃肿
- 自动化流程经常混线

那这个模式会很适合你。

---

## 核心理念

Mode A 第一版坚持几个原则：

- **你只和 main 说话**
- **main 负责调度，不负责包办一切**
- **先软分工，后硬隔离**
- **先做 3 个常驻 Agent，别一口气上 12 个**
- **看板负责观察，不负责抢主入口**

---

## 第一版的 4 个角色

### `main`
**唯一入口 / 总调度官**

职责：
- 理解用户需求
- 判断任务类型
- 调用 analyst / publisher / ops
- 汇总结果并统一回复风格

用户只需要和 `main` 对话。

---

### `analyst`
**分析师**

职责：
- A股盘面分析
- 指数与板块强弱判断
- 个股研究
- 商品 / 原油 / 猪价 / 宏观趋势分析

适合：
- 今天盘面怎么看
- 哪些板块强
- 某只股票有没有优势
- 哪些趋势股值得跟踪

---

### `publisher`
**发布官**

职责：
- 博客文章整理与发布
- frontmatter 校验
- GitHub push
- Cloudflare Pages 构建排查
- 复盘 txt/xlsx 发送链路

适合：
- 发一篇博客
- 为什么 Pages 没更新
- 为什么 frontmatter 报错
- 复盘文件为什么没发出去

---

### `ops`
**运维官**

职责：
- OpenClaw 网关 / cron / hook / config
- Docker / 宝塔 / 反代 / 域名 / 面板部署
- 服务器排障
- 自动化链路修复

适合：
- 为什么 main 不回消息
- 为什么 Dashboard 打不开
- 为什么 hook 没触发
- 为什么某个服务挂了

---

## 这和“三省六部”是什么关系？

这个方案受 `edict` 项目的启发，但并不直接照搬 12 个角色。

第一版只保留其精华：

- **分工**：分析 / 发布 / 运维分离
- **调度**：main 统一中转
- **可观察性**：看板可以看到这些 Agent 的状态
- **逐步演进**：后续再考虑 reviewer / 更复杂权限矩阵

也就是说，它是一个更**轻量、可落地、适合个人助手**的版本。

---

## 当前目录结构

```bash
agents/
├── analyst/
│   ├── SOUL.md
│   └── AGENTS.md
├── publisher/
│   ├── SOUL.md
│   └── AGENTS.md
└── ops/
    ├── SOUL.md
    └── AGENTS.md

docs/
├── mode-a-plan.md
├── skills-mapping.md
└── rollout-checklist.md
```

---

## 推荐实施顺序

### Step 1
创建 3 个常驻 Agent 的 workspace 与角色文件

### Step 2
注册 3 个常驻 Agent 到 OpenClaw 配置

### Step 3
验证主入口仍然是 `main`

### Step 4
做最小联调：
- main -> analyst
- main -> publisher
- main -> ops

### Step 5
把真实工作流逐步挂上去：
- 分析链
- 发布链
- 运维链

### Step 6
再考虑看板增强、reviewer、skills 白名单、权限矩阵

详见：
- [`docs/mode-a-plan.md`](docs/mode-a-plan.md)
- [`docs/skills-mapping.md`](docs/skills-mapping.md)
- [`docs/rollout-checklist.md`](docs/rollout-checklist.md)

---

## 使用方式（用户视角）

### 你不用学会多 Agent
你只需要像平常一样对 `main` 说：

- “分析一下今天盘面”
- “把这段发到博客”
- “帮我看服务器为什么不回消息”

然后：
- `main` 自己判断任务类型
- 后台派给对应 Agent
- 最后仍然由 `main` 统一回复你

这就是 Mode A 最重要的价值：

> **复杂度留在后台，体验保持单一入口。**

---

## 第一版的技能策略

第一版不建议一上来就做严格 skills 白名单，推荐：

### 公共技能池
所有 Agent 可共享：
- `multi-search-engine`
- `tavily`
- `summarize`
- `excel-xlsx`

### 专属技能方向
- `analyst`：财经 / 股票 / 数据分析类
- `publisher`：GitHub / 发布 / 自动化类
- `ops`：运维 / Docker / 配置 / 日志类

也就是说：

> 第一版先“职责分工”，第二版再“技能硬隔离”。

---

## 多 Agent 的第一条安全规则

### 注册新 Agent 后，必须立刻检查：
1. **Telegram DM 默认入口仍然是 `main`**
2. 主会话身份没有漂移
3. 子 Agent 不会抢主入口
4. 再继续做联调测试

这是这套方案里最关键的一条规则。  
任何时候，**主入口不能丢。**

---

## 这个仓库适合谁？

适合：
- 想保留“只和一个助手聊天”的体验
- 但又想享受后台专职分工的稳定性
- 希望一步步把单 Agent 系统演进成多 Agent 系统
- 不想一开始就被复杂编排框架绑死

不适合：
- 一开始就想做复杂组织模拟
- 追求炫技型 12+ Agent 展示项目
- 不在意稳定性和维护成本

---

## 后续演进方向

这个仓库后续可以继续发展为：

- reviewer（审核官）
- 更细的 Agent 权限矩阵
- skills 白名单硬隔离
- 面板驱动的任务观察和干预
- Telegram / 看板 更深整合

但第一版的核心目标不会变：

> **先把系统拆干净，再把系统做复杂。**

---

## License

MIT
