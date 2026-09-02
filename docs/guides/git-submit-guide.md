# 仓库提交引导（新人 + AI 通用）

> **本文档的双重用途**：
> 1. 新加入项目的伙伴按本文档完成环境准备和首次提交
> 2. AI 助手（CodeBuddy / Codex / Copilot 等）在协助提交操作时，**必须先读本文件**，按其中规范执行
>
> 上位规范见根目录 `AGENTS.md`，本文件只聚焦"提交到仓库"这一件事。

---

## 1. 仓库信息（往哪里提交）

| 项目 | 值 |
| --- | --- |
| 远程仓库 | `https://git.woa.com/oktang/Hero_Info_Platform` |
| 平台 | **腾讯工蜂**（企业内网 Git 平台，GitLab 基座）。开发内容涉及企业隐私，**严禁把代码推送到 GitHub 等外部平台** |
| 协议 | 工蜂同时支持 Git 与 SVN 协议访问，**本项目统一使用 Git** |
| 主干分支 | `main`（受保护，**禁止直推**，只接受 MR 合入） |
| 功能分支 | `feature/<简短描述>`，如 `feature/hero-list-page` |
| 修复分支 | `fix/<简短描述>` |

## 2. 需要安装的软件

| 软件 | 必装/可选 | 用途 | 下载 |
| --- | --- | --- | --- |
| **Git for Windows** | 必装 | Git 本体，一切操作的基础；自带 Git Credential Manager（凭据缓存）和 Git Bash | https://git-scm.com/download/win |
| **TortoiseGit** | 可选（推荐） | 右键菜单图形界面，提交/推送/看日志更直观；中文提交信息不会乱码 | https://tortoisegit.org/download/ |

> TortoiseGit 只是 Git 的图形外壳，底层调用同一个 Git，与命令行操作完全互通，可混用。
> 工蜂的 Issue/MR 管理走**工蜂网页端**（GitLab 界面），无需 GitHub CLI（`gh` 对工蜂无效）。

## 3. 首次接入步骤

```bash
# 1. 克隆仓库到本地（需要公司内网/VPN 环境）
git clone https://git.woa.com/oktang/Hero_Info_Platform.git

# 2. 进入项目
cd Hero_Info_Platform

# 3. 配置本仓库提交身份（重要！工蜂 committer-check 钩子校验提交邮箱，
#    非公司邮箱的提交会被拒绝。name 建议用英文名/RTX 名）
git config user.name "你的英文名"
git config user.email "你的英文名@tencent.com"
```

**认证方式**：
- HTTPS 推送时使用工蜂账号（RTX 域账号）认证，首次推送输入一次后由 Git Credential Manager 缓存，**此后免登录**
- 也可在工蜂个人设置里配置 **SSH Key**，然后把远程地址换成 SSH 形式，推送更稳定
- commit 是纯本地操作，从来不需要登录；只有 push/pull 联网操作需要认证

## 4. 日常提交流程

```bash
# 1. 开工前同步主干
git checkout main
git pull

# 2. 从主干切功能分支（单人单分支单任务）
git checkout -b feature/hero-list-page

# 3. 开发... 查看改动
git status
git diff

# 4. 提交（提交信息规范见第 5 节）
git add <文件>
git commit -F <提交信息文件>   # 推荐方式，见第 6 节编码坑

# 5. 推送并发起 MR
git push -u origin feature/hero-list-page
# 然后到工蜂网页发起 Merge Request 到 main，按模板填写（含「AI 参与说明」）
```

TortoiseGit 等价操作：文件夹右键 → `TortoiseGit` → `拉取(Pull)` / `切换/检出(Switch/Checkout)` / `提交(Commit)` / `推送(Push)`。

## 5. 提交信息规范（必须遵守）

- 格式：`<type>: <中文描述>`
- type 取值：`feat`（新功能）/ `fix`（修复）/ `docs`（文档）/ `refactor`（重构）/ `test`（测试）/ `chore`（构建工具）
- 示例：`feat: 新增英雄列表页`、`fix: 修复英雄详情接口空指针`
- **关联 TAPD 单号**：对应 TAPD 单子的提交在信息末尾带单号，如 `feat: 英雄树接口（TAPD-1012345）`，工蜂与 TAPD 联动后单子上自动出现提交记录
- **小步提交**：一个提交只做一件事，禁止把无关改动混入同一提交
- 描述用**简体中文**，一句话说明"做了什么"，不堆细节

## 6. 已知坑（AI 必读）

### 6.1 Windows 命令行中文提交信息乱码
PowerShell/CMD 把命令行参数按 GBK 编码传给 Git，直接 `git commit -m "中文"` 会得到乱码提交信息（如 `鏂板鍥㈤槦`）。

**正确做法（三选一）**：
1. 用 UTF-8 文件提交：
   ```bash
   git commit -F <提交信息文件.txt>   # 文件必须 UTF-8 编码
   ```
2. 用 TortoiseGit 的提交窗口直接输入中文（无乱码问题）
3. 用 Git Bash 而不是 PowerShell/CMD

**AI 助手注意**：在 Windows 上代用户执行中文提交时，一律走方式 1（写临时 UTF-8 文件 + `git commit -F`），提交后删除临时文件。

### 6.2 committer 邮箱被钩子拒绝
工蜂服务端有 committer-check 钩子：提交记录里的邮箱必须是公司邮箱（`@tencent.com`），否则 push 被拒。
现象：push 报 `committer` / `email` 相关拒绝信息。
处理：按第 3 节配置本仓库 `user.email` 后，对错误提交执行 `git commit --amend --reset-author`（未推送时）修正，再推。

### 6.3 其他
- 不要提交密钥、Token、`.env` 等敏感文件；`.gitignore` 已配置的不要强行 `git add -f`
- 企业隐私内容**严禁推送到任何外部平台**（GitHub/Gitee/个人网盘）
- 修改文件前先 `git pull`，减少冲突
- 推送被拒（non-fast-forward）说明远程有他人新提交，先 `git pull --rebase` 再推
- 禁止 `git push --force` 到 `main`；共享分支强推前必须团队确认

## 7. AI 助手操作清单（Checklist）

AI 在代用户执行提交操作时按此清单执行：

1. [ ] 读本文件与 `AGENTS.md` 第 7 节
2. [ ] `git status` 确认改动范围，核对是否与用户任务一致，不夹带无关文件
3. [ ] 确认当前分支；在 `main` 上时先切 `feature/` 或 `fix/` 分支
4. [ ] 提交信息符合第 5 节格式，中文走第 6.1 节的防乱码方式
5. [ ] 确认本仓库 `user.email` 为 `@tencent.com`（防 6.2 钩子拒绝）
6. [ ] Git 写操作（commit/push）需用户明确指令后执行，不主动提交
7. [ ] 推送失败时如实报告错误（认证被拒/钩子拒绝/冲突/网络），不反复重试、不强推
