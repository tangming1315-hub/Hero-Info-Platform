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
| 远程仓库 | `https://github.com/tangming1315-hub/Hero-Info-Platform` |
| 平台 | GitHub（**只支持 Git 协议**，已于 2024-01-08 关闭 SVN 支持，SVN 客户端一律不可用） |
| 主干分支 | `main`（受保护，**禁止直推**，只接受 PR 合入） |
| 功能分支 | `feature/<简短描述>`，如 `feature/hero-list-page` |
| 修复分支 | `fix/<简短描述>` |

## 2. 需要安装的软件

| 软件 | 必装/可选 | 用途 | 下载 |
| --- | --- | --- | --- |
| **Git for Windows** | 必装 | Git 本体，一切操作的基础；自带 Git Credential Manager（凭据缓存）和 Git Bash | https://git-scm.com/download/win |
| **TortoiseGit** | 可选（推荐） | 右键菜单图形界面，提交/推送/看日志更直观；中文提交信息不会乱码 | https://tortoisegit.org/download/ |
| GitHub CLI (`gh`) | 可选 | 命令行管理 PR/Issue | https://cli.github.com/ |

> TortoiseGit 只是 Git 的图形外壳，底层调用同一个 Git，与命令行操作完全互通，可混用。
> 安装 Git for Windows 时保持默认选项即可（默认已勾选凭据管理器）。

## 3. 首次接入步骤

```bash
# 1. 克隆仓库到本地（以你的工作目录为例）
git clone https://github.com/tangming1315-hub/Hero-Info-Platform.git

# 2. 进入项目
cd Hero-Info-Platform

# 3. 确认身份（GitHub 账号名和邮箱，一般全局已有配置可跳过）
git config user.name
git config user.email
```

**首次推送认证（只做一次）**：第一次执行 `git push` 时会弹出 GitHub 登录窗口，在窗口里完成浏览器授权。完成后凭据会存入 Windows 凭据管理器（Git Credential Manager），**此后命令行和 TortoiseGit 推送都不再需要登录**。

- 如果弹窗被关掉/取消，凭据不会被缓存，下次还会再弹 —— 重新推送并完成授权即可
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

# 5. 推送并发起 PR
git push -u origin feature/hero-list-page
# 然后到 GitHub 网页发起 Pull Request 到 main，按模板填写（含「AI 参与说明」）
```

TortoiseGit 等价操作：文件夹右键 → `TortoiseGit` → `拉取(Pull)` / `切换/检出(Switch/Checkout)` / `提交(Commit)` / `推送(Push)`。

## 5. 提交信息规范（必须遵守）

- 格式：`<type>: <中文描述>`
- type 取值：`feat`（新功能）/ `fix`（修复）/ `docs`（文档）/ `refactor`（重构）/ `test`（测试）/ `chore`（构建工具）
- 示例：`feat: 新增英雄列表页`、`fix: 修复英雄详情接口空指针`
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

### 6.2 其他
- 不要提交密钥、Token、`.env` 等敏感文件；`.gitignore` 已配置的不要强行 `git add -f`
- 修改文件前先 `git pull`，减少冲突
- 推送被拒（non-fast-forward）说明远程有他人新提交，先 `git pull --rebase` 再推
- 禁止 `git push --force` 到 `main`；共享分支强推前必须团队确认

## 7. AI 助手操作清单（Checklist）

AI 在代用户执行提交操作时按此清单执行：

1. [ ] 读本文件与 `AGENTS.md` 第 7 节
2. [ ] `git status` 确认改动范围，核对是否与用户任务一致，不夹带无关文件
3. [ ] 确认当前分支；在 `main` 上时先切 `feature/` 或 `fix/` 分支
4. [ ] 提交信息符合第 5 节格式，中文走第 6.1 节的防乱码方式
5. [ ] Git 写操作（commit/push）需用户明确指令后执行，不主动提交
6. [ ] 推送失败时如实报告错误（认证被拒/冲突/网络），不反复重试、不强推
