# OpenClaw Mode A Multi-Agent

一个适合个人助手场景的 **Mode A 多 Agent 协作方案**：

> 你只和主 Agent 对话，主 Agent 在后台调度多个常驻专职 Agent 完成分析、发布、运维等任务。

这个仓库是基于 OpenClaw 的一套 **轻量三省六部化实践**，适用于：
- A 股复盘与盘后发布
- 博客自动发布
- OpenClaw / 服务器 / Docker 运维排障
- 单人入口、多 Agent 协同

## 核心理念

- **你只和 main 说话**
- **main 负责调度**
- **analyst / publisher / ops 各司其职**
- **先软分工，后硬隔离**
- **看板负责观察，不抢主入口**

## 第一版角色

### main
- 唯一入口
- 负责理解需求、分配任务、汇总回复

### analyst
- 盘面分析
- 个股研究
- 板块强弱
- 商品/期货/宏观研判

### publisher
- 博客文章整理与发布
- frontmatter 校验
- GitHub push / Cloudflare Pages 排障
- 复盘 txt+xlsx 发送链路

### ops
- 服务器排障
- OpenClaw 网关 / hook / cron / config
- Docker / 宝塔 / 反代 / 面板部署

## 目录结构

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

## 使用方式

1. 在 OpenClaw 中注册常驻 Agent
2. 为每个 Agent 指定独立 workspace
3. 给 main 增加允许调度的 agent 白名单
4. 先进行最小联调测试
5. 再逐步把真实任务挂给 analyst / publisher / ops

## 推荐实施顺序

详见：
- `docs/mode-a-plan.md`
- `docs/rollout-checklist.md`
- `docs/skills-mapping.md`

## 安全提醒

### 多 Agent 注册后必须立即检查：
1. Telegram DM 默认入口仍然是 `main`
2. 主会话身份仍然是主 Agent
3. 子 Agent 不会抢占主入口
4. 再继续做联调测试

这是第一条强规则。

## 适合谁

- 想保留“只跟一个助手对话”的体验
- 但又希望后台有专职 Agent 分工
- 想逐步演进到更复杂的编排系统，而不是一上来就 12 个 Agent

## License

MIT
