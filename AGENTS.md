# AGENTS.md — Hero-Info-Platform 团队协作宪章

> 本文件是 AI 编程助手（CodeBuddy / Codex / Copilot / Cursor 等）与团队成员的共同约定。
> **写给 AI 看的约束，也是写给人的协作规则。** 修改本文件必须走 MR 流程，与代码同等对待。
> 技术栈确定后，请第一时间补齐文中所有 `TODO` 标记的章节。

---

## 1. 项目概述

- **项目名**：Hero-Info-Platform
- **定位**：英雄信息平台（TODO：补充一句话产品定位与目标用户）
- **仓库**：https://git.woa.com/oktang/Hero_Info_Platform （腾讯工蜂，企业内网，GitLab 基座）
- **目录结构**（TODO：技术栈确定后补充）
  ```
  Hero-Info-Platform/
  ├── AGENTS.md                  # 本文件：AI 与人的协作宪章
  ├── CLAUDE.md                  # Claude Code / CodeBuddy 类工具的核心约束入口
  ├── .gitlab/
  │   ├── issue_templates/       # 工蜂 Issue 模板（任务/缺陷）
  │   └── merge_request_templates/  # MR 模板（含 AI 参与说明）
  ├── docs/
  │   ├── agent-board/           # Agent 异步留言板
  │   └── guides/                # 提交引导、任务渠道规范
  ├── src/                       # TODO
  └── tests/                     # TODO
  ```

## 2. 环境搭建与构建测试命令

```bash
# TODO：技术栈确定后补齐以下命令（AI 会自动执行，写错=人人踩坑）
# 安装依赖：
# 本地启动：
# 构建：
# 运行全部测试：
# 运行单个测试：
# Lint：
```

**铁律**：提交 MR 前必须本地通过 Lint 和测试，AI 代理完成编码任务后必须自行执行上述命令验证。

## 3. 代码风格规范

> 以下写成**约束条件**，不是背景介绍。描述越具体，AI 遵守率越高。

- 文件命名：kebab-case（TODO：按技术栈调整）
- 类/组件命名：PascalCase
- 函数/变量命名：camelCase，函数名以动词开头
- 常量命名：UPPER_SNAKE_CASE
- 注释与提交信息：中文说明意图，不解释显而易见的行为
- 新增依赖前必须确认项目内没有现成封装，禁止随意引入第三方库

## 4. 架构约定

- TODO：技术栈与分层确定后补充，例如：
  - 分层职责边界（Controller 不写业务逻辑，必须下沉到 Service）
  - 数据访问统一走 Repository/DAO 层，不直接暴露 ORM 对象
  - 错误处理统一走公共错误类，禁止裸抛异常

## 5. 测试要求

- 新增功能必须带测试，覆盖主路径和边界情况
- 测试文件与源码同目录或镜像目录结构（TODO：按技术栈定）
- AI 生成代码后必须运行测试，失败必须修复后再交付

## 6. 安全红线（不可违反）

- **禁止**将任何密钥、Token、内部域名、个人凭据写入代码、注释、prompt 或提交记录
- 配置一律走环境变量或本地配置文件，`.env` 等敏感文件必须在 `.gitignore` 中
- 禁止在代码中硬编码内网地址、数据库连接串
- 对外部输入必须做校验，禁止拼接 SQL
- AI 代理遇到疑似敏感信息时必须停下来向用户确认，不得擅自提交

## 7. Git 协作流程

> **提交操作前必读**：[docs/guides/git-submit-guide.md](docs/guides/git-submit-guide.md) —— 软件安装、首次接入、提交规范、中文乱码等已知坑的完整引导（新人与 AI 通用）。

### 分支策略
- `main`：主干，受保护，只接受 MR 合入
- 功能分支：`feature/<简短描述>`，如 `feature/hero-list-page`
- 修复分支：`fix/<简短描述>`
- 单人单分支单任务，避免多人/多 AI 会话在同一分支并行

### 提交规范
- 提交信息格式：`<type>: <中文描述>`，type ∈ `feat | fix | docs | refactor | test | chore`
- 小步提交：一个提交只做一件事，AI 代理禁止把无关改动混入同一提交
- **committer 邮箱必须是公司邮箱（@tencent.com）**，工蜂 committer-check 钩子会拒绝非公司邮箱的提交

### MR 规范
- **所有代码（含 AI 生成）必须走 MR（Merge Request），禁止直推 main**
- MR 必须按模板填写「AI 参与说明」：哪些部分由 AI 生成、人工做了哪些验证
- MR 通过自动化检查（lint + test）与评审后才能合入
- 任务拆分原则：大需求拆成边界清晰、输入输出明确的子任务，一个 MR 对应一个子任务

### 并行协作冲突规避
- 开工前先 `git pull` 同步主干
- 跨模块改动先在群里/MR 中声明涉及文件，避免与他人任务撞车
- 发现 AI 改动了任务范围外的文件，必须停下确认

## 8. AI 协作规则（人与 AI 共同遵守）

> **Agent 间沟通一律走 [Agent Board](docs/agent-board/README.md)**（仓库内异步留言板，格式见 `docs/agent-board/TEMPLATE.md`）：开始工作前先看板收信，跨模块改动后必须到相关线程留言。
>
> **任务拆解/派发/跟踪一律走工蜂 Issues + 看板（Boards）**，方向性开放讨论走企业微信群或工蜂 Issue —— 渠道分工与操作规范见 [docs/guides/task-and-discussion-guide.md](docs/guides/task-and-discussion-guide.md)。（工蜂无 Discussions 功能）

1. **需求不猜方向**：需求有歧义或有多个方案时，先与人确认再动手
2. **先读后写**：修改任何文件前先阅读相关代码与规范，禁止凭空重写大文件
3. **产出即验证**：AI 交付前必须运行构建/测试/Lint，验证结果写进 MR 描述
4. **失败要留痕**：AI 踩过的坑、验证过的结论，沉淀到本文件或 `docs/` 下，供全团队复用
5. **本文件是活文档**：规范演进 = 修改本文件 + 提 MR + Review，禁止只在群里口头约定

## 9. 文档与知识沉淀

- 架构决策记录（ADR）：重要取舍放 `docs/adr/`，记录背景、选项、结论，不得静默覆盖历史决策
- 变更记录：功能级变更随 MR 更新对应文档
- TODO：确定后补充文档目录结构

---

*本文件遵循 [agents.md](https://agents.md) 开放格式，跨 AI 工具通用。用户在对话中的明确指令优先级最高，可覆盖本文件约定。*
