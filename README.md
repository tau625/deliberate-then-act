# 谋定后动（Deliberate-Then-Act）— dsh 规划/执行分工 Presets

> **谋定而后动，知止而有得。** ——《孙子兵法》
> **谋** = 规划会话（常驻，只谋不动）· **定** = 任务卡定型（证据/写域/验收锁死）· **后动** = 执行会话（谋定才动手，干完落盘即走）

把「**规划会话 / 执行会话**」分工机制打包成两个 dsh agent preset，让长任务的架构决策与编码执行解耦：规划会话常驻答疑评审，执行会话按任务卡干活、干完落盘即关。

> 配套文档在 [Xindex 仓库](https://github.com/tau625/Xindex)：
> `docs/HANDOVER.md`（现状与坑）、`docs/ROADMAP.md`（改进 backlog 与机制）、`docs/WORKER-BRIEF.md`（开工模板与分工契约）。

## 为什么叫「谋定后动」

这套机制的核心是**决策与执行解耦**：规划会话「谋定」（想清楚、写成卡），执行会话「后动」（照卡干、不留自由发挥空间）。结果通过 **git 提交 + 文档更新**回流，记忆活在仓库里而不是对话里——所以换会话不丢上下文，长任务不怕中断。

## 装什么

| preset | 角色 | 何时用 |
|---|---|---|
| **谋定后动 · 规划会话（Lead）** | 规划 / 答疑 / 评审 / 裁决，**不写代码** | 常驻：拆需求、排优先级、审 diff、答架构问题 |
| **谋定后动 · 执行会话（Worker）** | 按任务卡干活，**只做那一个任务** | 按需开：贴 WORKER-BRIEF §1 模板，干完关 |

## 安装（30 秒）

```powershell
# 把两个目录复制到 dsh 的 agent-presets 目录
Copy-Item -Recurse -Force xindex-plan, xindex-worker "$env:USERPROFILE\.dsh\.agent-presets\"
```

然后**重启 dsh / 新开会话**，在 agent preset 选择器里能看到两个新 preset。

## 用法

1. **开规划会话**（选 `Xindex 规划会话（Lead）`）：提你的想法（一句话即可），它产出任务卡（任务/证据/写域/验收）。
2. **开执行会话**（选 `Xindex 执行会话（Worker）`）：粘贴 `docs/WORKER-BRIEF.md` §1 模板并填入任务卡的四项；它按契约干活。
3. **回规划会话评审**：说「读 docs/ROADMAP.md §5 最新记录 + 提交 <sha>，评审一下」。
   结果通过 **git 提交 + 文档更新**回流，不需要两个对话同时在线。

## 三条铁律（preset 内置约束）

1. 文案/类串**逐字照抄**原版，不自创不改写
2. 每个改动都要有**前后数字证据**（像素差 / DOM 交集 / 文案覆盖 / 功能体检）
3. **运行时验证优先于静态检查**（esbuild 拦不住 ReferenceError/TDZ 类白屏）

## 模型配置提示

子代理/新会话默认走 `xiaomi-token-plan-cn / mimo-v2.6-flash`（`~/.dsh/settings.yaml.imported` 的 `agent-default-model`）。
**成员模型绑定是 spawn 时定死的**：改配置后必须重建成员；工具面没有删除成员的能力，**开新会话是唯一清 slot 手段**。

## 模板自定义

两个 preset 的 `agent.cordis.yml` 都是纯 persona 注入（`@deepseek-ai/dsh-persona` 的 `prefix`/`suffix`），改成你自己的项目名/文档路径即可复用到别的项目。

## License

MIT
