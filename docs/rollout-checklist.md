# 多 Agent 上线清单

## Step 1: 创建 workspace
- [ ] analyst workspace
- [ ] publisher workspace
- [ ] ops workspace
- [ ] 写入基础 SOUL.md / AGENTS.md

## Step 2: 注册 Agent
- [ ] 写入 OpenClaw agents.list
- [ ] 为 main 保留 default=true
- [ ] 分配独立 workspace
- [ ] 指定各自模型

## Step 3: 保护主入口
- [ ] Telegram DM 默认入口仍为 main
- [ ] 主会话身份正常
- [ ] 子 Agent 不会抢占主入口
- [ ] 再做联调测试

## Step 4: 最小联调
- [ ] main -> analyst
- [ ] main -> publisher
- [ ] main -> ops

## Step 5: 看板接入
- [ ] 看板正确显示 main / analyst / publisher / ops
- [ ] 不混入默认样板官员
- [ ] 状态可见

## Step 6: 试运行
- [ ] 分析链试运行
- [ ] 发布链试运行
- [ ] 运维链试运行

## Step 7: 后续优化
- [ ] reviewer
- [ ] skills 白名单
- [ ] 更细的权限矩阵
