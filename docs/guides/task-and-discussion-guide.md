# 任务派发与讨论渠道规范（人 + AI 通用）

> 本项目协作渠道的分工与使用规范。AI 助手在建任务、拆任务、派发、讨论前**必须读本文件**。
> 上位规范见 `AGENTS.md`；Agent 间日常沟通另见 `docs/agent-board/README.md`。

## 1. 渠道分工总表

| 需求 | 渠道 | 说明 |
| --- | --- | --- |
| 需求与排期管理（管理层视图） | **TAPD** | 需求/迭代/任务/缺陷单；工蜂提交与 MR 可关联 TAPD 单号双向联动（见 `docs/research/gongfeng-multi-agent-collab-research.md`） |
| 代码级任务拆解、派发、进度跟踪 | **工蜂 Issues + 看板（Boards）** | 开发执行视图，禁止口头/群聊派任务；看板按标签驱动分列 |
| Agent 间日常协作、代码旁留痕 | **Agent Board**（`docs/agent-board/`） | 随代码版本化，格式按 `docs/agent-board/TEMPLATE.md` |
| 方向性开放讨论、方案征询 | **Agent Board 线程（首选）** / TAPD 需求评论 / 企业微信群 | 工蜂无 Discussions 功能；Board 线程保持版本化可审计，排期人力类话题同步 TAPD，紧急情况企微群事后回填 Board |
| 具体代码变更的讨论 | **MR 评论** | 围绕单次变更，支持行级评论 |
| 项目文档沉淀 | **`docs/`** | 结论必须落到文档，不留存在聊天里 |

## 2. Issues 任务规范（工蜂）

### 建任务
- 一律使用 Issue 模板（`.gitlab/issue_templates/` 下 `任务` / `缺陷`），标题前缀 `[任务]` / `[缺陷]`
- **大任务必须拆解**：正文用 `- [ ]` 任务清单列出子任务；子任务较大时单独建子 Issue，并在父子 Issue 正文里互相贴链接（工蜂无一键转子 Issue 功能）
- 每个任务**必须有负责人（assignee）**，未派发的任务放 Todo 列等派
- 验收标准必须可验证（能跑测试/能演示），禁止写"完成 xxx 开发"这种无法判定的标准

### 派任务
- 派给人：assignee 设为对方工蜂账号，并在 Issue 里 @ 说明期望时间
- 派给 AI Agent：assignee 设为主人账号，正文注明执行 Agent 标识与完成后的汇报方式（见第 4 节）

### 追任务
- 状态走**工蜂看板（Boards）**：`Todo → In Progress → In Review → Done`，开工/提交 MR/合入时及时挪动（看板按标签驱动，列与标签一一对应）
- MR 描述里关联 Issue（`Closes #N`），合入后自动关闭

### 标签约定
| 标签 | 用途 |
| --- | --- |
| `task` / `bug` | 类型（模板自动带） |
| `priority-high` / `priority-low` | 优先级 |
| `agent-doing` | 由 AI Agent 执行中 |
| `need-decision` | 卡在决策点，需要 Owner 裁决 |

## 3. 开放讨论规范（工蜂无 Discussions 的替代方案）

- 用于**方向性、开放性**议题：技术选型讨论、规范修订征询、里程碑回顾等
- 三种载体按场景选：
  - **Agent Board 线程（首选）**：需要留痕、跨天持续的开放话题；保持版本化 + 可审计，结论归档 `decisions/`
  - **TAPD 需求/任务评论**：涉及排期与人力的讨论
  - **企业微信群**：需要即时响应的紧急情况，事后把结论回填 Board
- **讨论出结论后必须转化**：结论沉淀为 `docs/` 文档、转为任务 Issue 或归档 `decisions/`，并在原讨论处标注结论链接后关闭
- 不用于任务派发（无状态跟踪），不用于代码级讨论（去 MR 或 Agent Board）

## 4. AI Agent 操作规范

1. **建/改任务**：AI 代用户操作工蜂 Issue 时，优先通过工蜂网页端（AI 输出规范化文本由用户粘贴），或经授权后调用工蜂 openAPI；**GitHub 的 `gh` CLI / GitHub MCP 对工蜂无效**
2. **标明身份**：AI 创建的 Issue/评论必须在末尾注明 `— by <Agent 标识>`，保证可溯源
3. **执行中被派任务**：开工把 Issue 挪到 In Progress 并加 `agent-doing` 标签；完成发 MR 后挪 In Review；卡住加 `need-decision` 并 @ Owner
4. **汇报闭环**：Agent 完成任务后在 Issue 评论汇报（做了什么/验证结果/MR 链接），禁止静默完工
5. **拆任务先确认**：AI 把大需求拆成子任务清单后，先给用户确认再批量建 Issue

## 5. 与 Agent Board 的边界

- **Board 管"过程沟通"，Issue 管"任务状态"**：讨论接口怎么改 → Board 线程；谁负责改、改完没 → Issue + 看板
- Board 线程中达成共识形成任务时，在线程内贴 Issue 链接；Issue 里也回链 Board 线程，双向可追
