# CLAUDE.md — Hero-Info-Platform

> Claude Code / CodeBuddy 类工具的核心约束入口。**完整规范见 [AGENTS.md](./AGENTS.md)**，本文件只保留每次会话必须遵守的核心约束，保持精简。

## 核心约束（每次会话必读）

1. 遵守 `AGENTS.md` 全部约定；本文件与 AGENTS.md 冲突时以 AGENTS.md 为准，用户当次对话的明确指令优先级最高
2. 需求有歧义或多方案时，先向用户确认方向，**禁止猜方向执行**
3. 修改文件前先读相关代码；禁止重写未读过的大文件，用最小化改动完成任务
4. 交付前必须运行验证命令（见 AGENTS.md 第 2 节，技术栈确定后更新）：
   ```bash
   # TODO: lint / test 命令
   ```
5. **安全红线**：禁止写入密钥、凭据、内网地址；敏感配置走环境变量
6. 提交走 `feature/`、`fix/` 分支 + MR（工蜂 Merge Request），禁止直推 `main`；提交信息格式 `<type>: <中文描述>`；**committer 邮箱必须是公司邮箱 @tencent.com**（工蜂钩子校验）
7. AI 生成内容在 MR 中必须显形（填 MR 模板的「AI 参与说明」）
8. 踩过的坑与验证过的结论，沉淀回 `AGENTS.md` 或 `docs/`，不得只留在会话里
9. **Agent 间沟通走 [Agent Board](docs/agent-board/README.md)**：开工前看板收信，跨模块改动后到相关线程留言，格式按 `docs/agent-board/TEMPLATE.md`

## 项目速览

- 定位：英雄信息平台（TODO：补充）
- 技术栈：TODO
- 目录：`src/`、`tests/`、`docs/`（TODO：按实际结构更新）
