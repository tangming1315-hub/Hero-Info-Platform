# 工蜂仓库多人 + 多 Agent 协同开发调研报告

> 调研对象：https://git.woa.com/oktang/Hero_Info_Platform（英雄进度信息监控平台）
> 调研日期：2026-09-02
> 前置材料：本工作区 `AGENTS.md`、`docs/agent-board/`、`docs/guides/`、`publish/hero-platform-dev-plan.md`
>
> 说明：仓库页面需 iOA 内网认证，未能直接抓取内容；本报告基于工蜂（GitLab 基座）公开功能面 + 本仓库已沉淀的协作框架推导，落地前需在仓库设置页逐项核对开启状态（见第 8 节检查清单）。

---

## 0. 结论速览

1. **现有协作框架 90% 可平移**：`AGENTS.md` 宪章、Agent Board（仓库内留言板）、消息模板都是平台无关的，随仓库搬到工蜂即可用，只需把 "PR" 改叫 "MR"、把 "GitHub Issues/Projects/Discussions" 映射到工蜂对应物。
2. **工蜂没有 Discussions**：方向性讨论改走 **TAPD 需求/任务评论** 或 **Agent Board 线程**（推荐后者，继续留在仓库里版本化）。
3. **任务源建议上 TAPD**：工蜂 Issue 适合做代码级小任务与缺陷跟踪，但本项目的计划书已明确以 TAPD 任务单为关键数据源，且工蜂与 TAPD 有官方双向联动（提交关联、状态回写）。多人 + 多 Agent 场景下，**TAPD 管需求与排期、工蜂 Issue 管代码任务与缺陷** 的双层模型最顺。
4. **验收收口在 MR + CI**：工蜂支持保护分支 + MR 评审人规则 + CI 流水线状态卡控，把「lint/test 通过 + 人工 approve + AI 参与说明填写」设为合入门槛即可。
5. **Agent 上工蜂需要独立身份**：每个 Agent 用独立账号或项目级 Access Token 操作，禁止共用人号，保证审计可溯源。

---

## 1. 平台功能映射：GitHub 方案 → 工蜂方案

当前仓库文档全部按 GitHub 写的，平移到工蜂时的对应关系：

| 现有约定（GitHub） | 工蜂对应物 | 差异与注意 |
| --- | --- | --- |
| Pull Request | **Merge Request（MR）** | 概念一一对应；工蜂 MR 支持评审人（Reviewer/Approver）、强制评审人数、CI 通过才可合入 |
| Issues + Projects 看板 | **工蜂 Issue + 看板（Board）** | GitLab 系看板按 Label 分列（如 `Todo`/`Doing`/`Review`/`Done` 用 label 驱动），不是独立 Projects 对象；里程碑（Milestone）对应 M0~M5 |
| Discussions | **无** | 替代：Agent Board 线程（仓库内，推荐）或 TAPD 需求评论区 |
| PR 模板 | **MR 模板**（`.gitlab/merge_request_templates/` 或仓库设置默认描述） | 「AI 参与说明」字段原样保留 |
| Issue 模板（`.github/ISSUE_TEMPLATE/`） | **Issue 模板**（`.gitlab/issue_templates/`） | 模板文件需迁移目录 |
| `gh` CLI / GitHub MCP | **工蜂 Open API**（OAuth2.0）+ `glab` 类工具或裸 API | 工蜂 API 与 GitLab API 高度相似；另有腾讯自研 `teamai-cli` 原生支持 tgit provider（可批量管理 Agent 账号权限，见第 6 节） |
| 分支保护 + PR 合入 | **保护分支 + MR** | 工蜂支持 main 保护、禁止直推、强制 MR，规则相同 |
| GitHub Actions | **工蜂 CI**（GitLab CI 兼容，`.gitlab-ci.yml`） | lint/test 流水线平移 |
| 代码关联 TAPD | **官方深度集成**（工蜂强项） | 提交/MR 关联 TAPD 需求、任务、缺陷单，状态双向可见 |

---

## 2. 需要什么规范（规范体系总图）

在现有规范基础上，针对「多人 + 多 Agent + 工蜂」补齐以下五层：

```
AGENTS.md（宪章，平台无关，平移即可）
├── 身份层：Agent 身份注册表（新增，见 2.1）
├── 沟通层：docs/agent-board/（平移，无需改）
├── 任务层：docs/guides/task-and-discussion-guide.md（改造为 TAPD + 工蜂 Issue 双层）
├── 提交层：docs/guides/git-submit-guide.md（改造为工蜂地址 + MR 流程）
└── 验收层：publish/hero-platform-dev-plan.md 里程碑出口标准（平移，作为验收依据）
```

### 2.1 需要新增的规范（当前没有的）

| 规范 | 内容 | 理由 |
| --- | --- | --- |
| **Agent 身份注册表** | `docs/agent-board/AGENTS-ROSTER.md`：登记每个 Agent 的标识（如 `Agent-张（后端）`）、对应工蜂账号/Token、负责模块、主人是谁 | 工蜂 MR/Issue 上的操作者是账号，Board 上是标识，需要一张对照表才能审计「这个 MR 是谁的 Agent 干的」 |
| **MR 评审人规则** | 仓库设置：main 保护分支 + 至少 1 名人类 Approver + CI 绿才可合入；Agent 不能被设为 Approver | 防止 Agent 自审自合，验收权永远在人手里 |
| **TAPD ↔ 工蜂关联格式** | 提交信息约定带 TAPD 单号（如 `feat: 英雄树接口（TAPD-1012345）`），MR 描述首行挂 TAPD 单链接 | 工蜂与 TAPD 联动后，单子上自动出现提交记录，进度回写有据 |
| **Agent 操作边界清单** | Agent 在工蜂上允许：建/改 Issue、发 MR、评论；禁止：改仓库设置、动保护分支、approve MR、删他人分支 | 权限最小化，出问题可追责 |
| **冲突裁决流程** | Board 已有「冲突找裁决」铁律，补一条：工蜂 MR 层面出现同一文件并行 MR 时，先合入者优先，后到者 rebase，禁止互相 close 对方 MR | 多 Agent 并行改代码的必然冲突点 |

### 2.2 需要修改的规范

- `git-submit-guide.md`：远端地址改为 `git.woa.com`、PR → MR、认证方式改为工蜂账号（或 UGit 客户端）；Windows 中文乱码、小步提交等坑位条款全部保留。
- `task-and-discussion-guide.md`：渠道分工表按第 1 节映射重写，新增 TAPD 一行。

---

## 3. Agent 之间如何交流讨论

**结论：维持 Agent Board 为默认渠道，工蜂侧只补两类场景。**

| 场景 | 渠道 | 说明 |
| --- | --- | --- |
| Agent 间日常协作、跨模块改动留痕、任务交接 | **Agent Board**（`docs/agent-board/`，平移） | 随 Git 版本化、零设施、人可审计；工蜂上看板和代码在同一仓库，`git pull` 即收件的体验不变 |
| 围绕某次代码变更的讨论 | **工蜂 MR 评论** | 支持行级评论（Diff Discussion），讨论未解决可阻塞合入（GitLab 系 " unresolved threads 不可合并" 开关，建议开启） |
| 围绕某个任务/缺陷的进度问答 | **工蜂 Issue 评论 或 TAPD 单评论** | Issue 管代码任务状态，TAPD 管需求进度；Agent 完成汇报写到 Issue 评论并同步 TAPD |
| 方向性开放讨论（原 Discussions 场景） | **Agent Board 线程 → 结论归档 `decisions/`**；涉及排期与人力的同步到 TAPD | 工蜂无 Discussions，Board 线程是唯一保持「版本化 + 可审计」的替代品 |
| 需要人实时介入的紧急情况 | 企微群 @ 人，事后把结论回填 Board | Board 是异步设施，不替代即时通讯 |

Board 的消息模板（`TEMPLATE.md`）、决策归档规则（`decisions/` 只追加不改写）原样保留——这套设计本身就是为多 Agent 异步协作做的，与平台无关。

---

## 4. 如何一起规划计划任务、拆分任务、分派任务

### 4.1 规划：双层任务源

```
publish/hero-platform-dev-plan.md（计划书：里程碑 M0~M5、WBS、出口标准）
        │
        ├─→ TAPD 项目：需求 / 迭代 / 任务 / 缺陷（排期、人力、进度上报，管理层视图）
        │        ↑ 官方联动：工蜂提交/MR 自动挂到 TAPD 单
        └─→ 工蜂 Issue + 看板 + Milestone：代码级任务（开发执行视图）
                 ↑ Agent Board 线程：任务怎么做的过程讨论
```

- **计划书是唯一事实源**：M0~M5 与 WBS 已写好，拆任务从它出发，不在群里口头拆。
- **里程碑映射**：工蜂建 M0~M5 六个 Milestone，每个 Issue 挂到对应 Milestone，看板燃尽图直接可用。
- **规划会议产物**：里程碑启动时由 Owner（人）+ 各 Agent 在 Board 开一个「Mx 规划线程」，把任务拆分结论留在仓库里，再批量建单。

### 4.2 拆分：沿用「一个任务包 = 一个 MR 边界」

计划书 WBS 已按此原则拆好（如 M1 = 树结构配置模型 / 进度上卷引擎 / TAPD/iWiki 适配器）。落到工蜂时的拆分规则：

1. 一个 Issue 对应一个可独立交付的任务包，验收标准可验证（能跑测试/能演示）——沿用现有 Issue 规范。
2. 大任务在 Issue 正文用 `- [ ]` 清单列子任务；子任务大到有独立 MR 边界时拆为子 Issue（GitLab 系支持 Issue 关联/父子）。
3. **AI 拆任务先确认**：Agent 把大需求拆成子任务清单后，先给 Owner 确认再批量建单——现有规范第 5 条原样保留。

### 4.3 分派

| 派给谁 | 做法 |
| --- | --- |
| 派给人 | 工蜂 Issue assignee 设对方账号；TAPD 单处理人设对方；两处保持一致 |
| 派给 Agent | Issue assignee 设为 **Agent 自己的工蜂账号**（不是主人账号——这正是要独立身份的原因），正文注明 Agent 标识与汇报方式；TAPD 处理人可仍挂主人，备注「由 Agent-X 执行」 |
| 状态流转 | 看板列（label 驱动）：`Todo → Doing → Review → Done`；Agent 开工挪 Doing 并加 `agent-doing` 标签，发 MR 挪 Review，卡住加 `need-decision` 并 @ Owner |

---

## 5. 如何验收功能、检查

### 5.1 验收三级（沿用现有思路，落到工蜂设施）

| 级别 | 执行者 | 设施 |
| --- | --- | --- |
| L1 自检 | 开发 Agent 自己 | 本地跑 lint/test（`AGENTS.md` 第 2 节命令，技术栈定后补齐）；结果写进 MR 描述 |
| L2 机检 | **工蜂 CI 流水线** | `.gitlab-ci.yml`：lint + 单测 + 构建；CI 红 = 不可合入（仓库设置强制） |
| L3 人验 | 人类 Approver | MR 评审（含「AI 参与说明」核对）+ 里程碑出口标准对照（计划书 Acceptance 章） |

### 5.2 关键卡控项（工蜂仓库设置）

- main 设为保护分支，禁止直推、禁止强推
- MR 合入条件：CI 通过 + 至少 1 名人类 Approver + 所有评论线程已解决
- MR 模板默认包含：变更说明 / **AI 参与说明**（哪些由 AI 生成、人工验证了什么）/ 关联 Issue 与 TAPD 单 / 验证结果
- 里程碑出口验收：M0~M5 出口标准逐条核对，不达标不进下一阶段（计划书已定）

---

## 6. 提交 Bug、修复 Bug 流程

### 6.1 提交 Bug

- **入口二选一**：用户侧/进度侧问题 → TAPD 缺陷单；代码级缺陷 → 工蜂 Issue（`bug` 标签 + 缺陷模板）
- 缺陷模板必填：复现步骤 / 期望与实际 / 影响范围 / 关联模块；Agent 代为建单时末尾署名 `— by <Agent 标识>`
- Agent 在开发/检查中**自己发现**的 bug：先建 Issue 留痕再修，禁止「顺手改了不提单」——缺陷数据是健康度统计的输入

### 6.2 修复 Bug

```
Issue（bug）→ 切 fix/<简短描述> 分支 → 修复 + 补回归测试
→ 提交信息：fix: 修复xxx（关联 Issue #N / TAPD 缺陷单号）
→ 发 MR → CI 绿 + 人工 approve → 合入自动关 Issue → 看板挪 Done
```

- 回归测试必须随修复一起提交（`AGENTS.md` 第 5 节）
- P0/P1 缺陷走加急通道：`priority-high` 标签 + @ Owner，M4 试运行期要求「连续 2 周无 P0/P1」（计划书出口标准）

---

## 7. Agent 在工蜂上的身份与权限（多 Agent 落地的关键）

| 项 | 建议 |
| --- | --- |
| 账号 | 每个 Agent 一个独立工蜂账号（或项目组批量开的 bot 账号），登记到 Agent 身份注册表；禁止共用人号 |
| API 操作 | Agent 代操作 Issue/MR 走工蜂 Open API（OAuth2.0），Token 走环境变量/本地配置，**不入库**（安全红线不变） |
| 权限 | Agent 账号给 Developer 角色（可推分支、发 MR、操作 Issue）；**不给 Maintainer**（不能改保护分支与仓库设置、不能 approve） |
| 批量管理 | 腾讯自研 `teamai-cli` 原生支持 tgit provider（git.woa.com），可按 user group 批量授权、统一管理 Agent 账号与仓库——Agent 数量上来后值得引入 |
| 审计 | 工蜂操作日志 + Git 历史 + Board 留言三处互证；出问题时按「MR 作者账号 → 注册表 → Agent 标识 → 主人」追责 |

---

## 8. 落地检查清单（开工前在工蜂仓库逐项核对）

- [ ] 仓库设置：main 保护分支（禁直推/禁强推）已开
- [ ] MR 合入条件：CI 通过 + ≥1 人类 Approver + 评论线程全解决
- [ ] Issue 模板（`.gitlab/issue_templates/`：任务.md / 缺陷.md）、MR 模板已入库
- [ ] 看板列（Todo/Doing/Review/Done）与标签（`task`/`bug`/`agent-doing`/`need-decision`/`priority-high`）已建
- [ ] Milestone M0~M5 已建
- [ ] 工蜂 CI（`.gitlab-ci.yml`）已配 lint/test（技术栈定后）
- [ ] TAPD 项目与工蜂仓库的代码关联已配置并验证（发一个测试提交看 TAPD 单是否出现记录）
- [ ] Agent 账号已建、Developer 权限已授、身份注册表已入库
- [ ] `AGENTS.md` / `git-submit-guide.md` / `task-and-discussion-guide.md` 中的 GitHub 表述已完成工蜂化改写并走 MR 合入
- [ ] 双仓库策略已拍板：GitHub 仓库与工蜂仓库是「迁移」还是「双 remote 同步」，唯一事实源是哪个（**建议尽快拍板，避免双写漂移**）

---

## 9. 开放问题（需你拍板）

| # | 问题 | 选项 |
| --- | --- | --- |
| Q1 | 唯一事实源仓库 | A. 全部迁工蜂，GitHub 只读镜像；B. 双 remote 双写（不推荐）；C. 维持 GitHub 为主 |
| Q2 | 任务源以谁为准 | A. TAPD 为主、工蜂 Issue 为辅（推荐）；B. 纯工蜂 Issue；C. 纯 TAPD |
| Q3 | Agent 账号形态 | A. 每 Agent 独立 bot 账号（推荐）；B. 项目级 Access Token 共用人号（审计弱） |
| Q4 | 是否引入 `teamai-cli` 管理 Agent 账号 | A. 引入；B. 账号少时先手工管理 |
