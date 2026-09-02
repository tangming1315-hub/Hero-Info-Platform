<div id="top" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;background:linear-gradient(135deg,#0f172a 0%,#1d4ed8 55%,#38bdf8 100%);border-radius:20px;padding:42px 36px 34px;margin-bottom:28px;color:#ffffff;position:relative;overflow:hidden;">
  <div style="position:absolute;top:-38px;right:-38px;width:180px;height:180px;background:rgba(255,255,255,0.12);border-radius:50%;"></div>
  <div style="position:relative;">
    <div style="font-size:13px;font-weight:700;letter-spacing:2px;text-transform:uppercase;opacity:0.82;margin-bottom:12px;">Project Plan · 2026-09</div>
    <div style="font-size:42px;font-weight:800;line-height:1.12;letter-spacing:-1px;margin-bottom:14px;">英雄进度信息监控平台<br>项目开发计划书</div>
    <div style="font-size:16px;line-height:1.8;max-width:860px;opacity:0.94;">基于《项目英雄进度信息监控平台开发方案》调研整理，覆盖项目背景与目标、需求范围拆解、技术选型与架构、里程碑计划、任务拆解（WBS）、风险预案与验收标准，作为立项与排期的统一依据。</div>
    <div style="margin-top:22px;display:flex;flex-wrap:wrap;gap:10px;">
      <a href="#milestones" style="display:inline-block;background:rgba(255,255,255,0.18);color:#ffffff;font-size:14px;font-weight:700;padding:10px 18px;border-radius:999px;text-decoration:none;">里程碑计划</a>
      <a href="#wbs" style="display:inline-block;background:rgba(255,255,255,0.10);color:#ffffff;font-size:14px;font-weight:700;padding:10px 18px;border-radius:999px;text-decoration:none;">任务拆解</a>
      <a href="#research" style="display:inline-block;background:rgba(255,255,255,0.10);color:#ffffff;font-size:14px;font-weight:700;padding:10px 18px;border-radius:999px;text-decoration:none;">调研与开放问题</a>
      <a href="#risks" style="display:inline-block;background:rgba(255,255,255,0.10);color:#ffffff;font-size:14px;font-weight:700;padding:10px 18px;border-radius:999px;text-decoration:none;">风险与依赖</a>
    </div>
  </div>
</div>

<div id="overview" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:8px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#2563eb;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Overview</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">项目背景与目标</div>
  <div style="font-size:16px;line-height:1.85;color:#64748b;max-width:860px;">英雄开发涉及配置、特效、角色、动画、相机系统、UI、音频等多条职能线并行，进度分散在 TAPD 任务单、引擎工程资产与各类规范文档中，缺乏统一视图。本平台以「英雄」为根节点构建进度树，一眼看清各职能当前进度、卡点位置与资产健康状况。</div>
</div>

<div style="display:flex;flex-wrap:wrap;gap:16px;margin-bottom:38px;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;">
  <div style="width:calc(50% - 8px);min-width:260px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:22px;border:1.5px solid #dbeafe;box-shadow:0 6px 24px rgba(59,130,246,0.06);">
    <div style="font-size:18px;font-weight:800;color:#0f172a;margin-bottom:10px;">目标一 · 查看进度</div>
    <div style="font-size:15px;line-height:1.8;color:#64748b;">交互式平台监控每个英雄的开发进度，细化到生产环节：一眼清楚各职能当前进度，哪一步做完了、哪一步没做完、卡在哪个步骤。</div>
  </div>
  <div style="width:calc(50% - 8px);min-width:260px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:22px;border:1.5px solid #dbeafe;box-shadow:0 6px 24px rgba(59,130,246,0.06);">
    <div style="font-size:18px;font-weight:800;color:#0f172a;margin-bottom:10px;">目标二 · 资产健康反馈</div>
    <div style="font-size:15px;line-height:1.8;color:#64748b;">开发步骤细化到资产生产阶段后，将生产规范与工程规范的健康程度可视化：节点关联规范文档，AI 从中提取检查项，制作规范检查流程工具，把健康结果反馈到平台展示（红 / 橙 / 绿）。</div>
  </div>
  <div style="width:calc(50% - 8px);min-width:260px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:22px;border:1.5px solid #fbcfe8;box-shadow:0 6px 24px rgba(236,72,153,0.06);">
    <div style="font-size:18px;font-weight:800;color:#0f172a;margin-bottom:10px;">LOQ 阶段规则</div>
    <div style="font-size:15px;line-height:1.8;color:#64748b;">每个节点携带「完成进度 + 当前 LOQ 阶段」。上卷规则：当所有子层级内容都满足 L2 时，父层级才会被判定为 L2，依次类推，最终在英雄根节点呈现整体完成度与 LOQ。</div>
  </div>
  <div style="width:calc(50% - 8px);min-width:260px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:22px;border:1.5px solid #fbcfe8;box-shadow:0 6px 24px rgba(236,72,153,0.06);">
    <div style="font-size:18px;font-weight:800;color:#0f172a;margin-bottom:10px;">关键数据源</div>
    <div style="font-size:15px;line-height:1.8;color:#64748b;">TAPD 任务单（阶段与详细进度）、iWiki 规范文档（检查项来源）、引擎工程资产（资产制作与内部资产挂接状态、规范检查结果）。</div>
  </div>
</div>

<div id="scope" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:20px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#2563eb;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Scope</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">需求范围 · 功能拆解</div>
  <div style="font-size:16px;line-height:1.85;color:#64748b;max-width:860px;">以方案文档中的英雄树状图为蓝本，拆解为六大功能模块。英雄树根节点下挂七条职能线：配置、特效、角色、动画、相机系统、UI、音频，每条职能线下挂各自的生产环节节点。</div>
</div>

<div style="display:flex;flex-wrap:wrap;gap:16px;margin-bottom:38px;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;">
  <div style="width:calc(33.3% - 11px);min-width:240px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:20px;border:1.5px solid #dbeafe;">
    <div style="font-size:16px;font-weight:800;color:#0f172a;margin-bottom:8px;">F1 英雄进度树</div>
    <div style="font-size:14px;line-height:1.8;color:#64748b;">树状交互视图：英雄 → 职能线 → 生产环节 → 叶子任务。节点展示完成进度、LOQ 阶段、负责人、资产健康度；支持展开/收起与节点点击跳转。</div>
  </div>
  <div style="width:calc(33.3% - 11px);min-width:240px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:20px;border:1.5px solid #dbeafe;">
    <div style="font-size:16px;font-weight:800;color:#0f172a;margin-bottom:8px;">F2 进度与 LOQ 聚合</div>
    <div style="font-size:14px;line-height:1.8;color:#64748b;">叶子节点进度采集 + 逐层上卷：按 LOQ 规则计算父层级阶段，根节点输出英雄整体完成进度与当前 LOQ。</div>
  </div>
  <div style="width:calc(33.3% - 11px);min-width:240px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:20px;border:1.5px solid #dbeafe;">
    <div style="font-size:16px;font-weight:800;color:#0f172a;margin-bottom:8px;">F3 TAPD 任务集成</div>
    <div style="font-size:14px;line-height:1.8;color:#64748b;">「技能设计」类节点关联 TAPD 任务单，从 TAPD 拉取所处阶段与详细进度；节点支持点击跳转到对应单子。</div>
  </div>
  <div style="width:calc(33.3% - 11px);min-width:240px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:20px;border:1.5px solid #dbeafe;">
    <div style="font-size:16px;font-weight:800;color:#0f172a;margin-bottom:8px;">F4 资产健康检查</div>
    <div style="font-size:14px;line-height:1.8;color:#64748b;">「技能制作」类节点关联规范文档，AI 提取检查项生成检查流程工具，对引擎内资产执行生产规范与工程规范检查，输出红 / 橙 / 绿健康度。</div>
  </div>
  <div style="width:calc(33.3% - 11px);min-width:240px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:20px;border:1.5px solid #dbeafe;">
    <div style="font-size:16px;font-weight:800;color:#0f172a;margin-bottom:8px;">F5 树结构配置化</div>
    <div style="font-size:14px;line-height:1.8;color:#64748b;">英雄树的生产环节结构（如角色线下的蓝图/骨骼/物理资产/材质，动画线下的 AT 表/同步组/3C 蓝图等）以配置描述，新英雄按模板实例化。</div>
  </div>
  <div style="width:calc(33.3% - 11px);min-width:240px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:20px;border:1.5px solid #dbeafe;">
    <div style="font-size:16px;font-weight:800;color:#0f172a;margin-bottom:8px;">F6 跳转与文档关联</div>
    <div style="font-size:14px;line-height:1.8;color:#64748b;">节点级外链：点击跳转 TAPD 单子、跳转规范文档，打通「看进度 → 查卡点 → 翻规范」的完整动线。</div>
  </div>
</div>

<div id="arch" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:20px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#2563eb;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Architecture</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">技术方案 · 选型与架构</div>
  <div style="font-size:16px;line-height:1.85;color:#64748b;max-width:860px;">三层架构：数据采集层对接 TAPD / iWiki / 引擎工程；聚合服务层维护英雄树模型并计算进度与健康度；展示层提供交互式树视图。技术选型为调研建议，立项评审时最终拍板。</div>
</div>

| 分层 | 模块 | 职责 | 选型建议 |
| --- | --- | --- | --- |
| 展示层 | 树视图前端 | 交互式进度树渲染、节点展开/跳转 | React + 树图组件（antv G6 / ECharts tree） |
| 聚合服务层 | 树模型服务 | 英雄树配置、进度上卷、LOQ 判定 | Node.js / Python FastAPI |
| 聚合服务层 | 健康度服务 | 检查项管理、检查任务调度、结果入库 | 同上，结果存 SQLite/MySQL |
| 数据采集层 | TAPD 适配器 | 拉取任务单阶段与进度 | TAPD 开放平台 API（api.tapd.cn，API 账号鉴权） |
| 数据采集层 | iWiki 适配器 | 拉取规范文档，AI 提取检查项 | iWiki 接口 + AI 提取流水线 |
| 数据采集层 | 资产扫描器 | 引擎工程资产状态与规范检查 | UE 工程内检查工具（Python/Editor 脚本） |

<div style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;background:#ffffff;border-radius:14px;padding:20px 22px;border:1.5px solid #dbeafe;margin:20px 0 30px;">
  <div style="font-size:15px;font-weight:800;color:#1e3a8a;margin-bottom:8px;">架构要点（含 TAPD 接入调研结论）</div>
  <div style="font-size:14px;line-height:1.9;color:#64748b;">① TAPD 接入路径已调研明确：鉴权用 Basic Auth（应用ID:应用秘钥，创建应用即生成，只调接口无需上架应用；非项目管理员需复制授权链接给项目管理员授权）；任务接口 <span style="font-family:'Consolas','Courier New',monospace;">GET /tasks</span> 返回 <span style="font-family:'Consolas','Courier New',monospace;">progress</span>（进度 0–100）、<span style="font-family:'Consolas','Courier New',monospace;">status</span>（open/progressing/done）、<span style="font-family:'Consolas','Courier New',monospace;">owner</span>、工时等字段，直接支撑节点进度采集；状态中文映射走 <span style="font-family:'Consolas','Courier New',monospace;">/workflow/status_map</span>；分页 limit≤200，配 count 接口取总数。② IDC → OA 网络受限有官方解法三选：IP + Host 头直连、专用域名 <span style="font-family:'Consolas','Courier New',monospace;">oss.apiv2.tapd.woa.com</span>、123 平台或 Golang 配置 Host 头。③ 实时性可选 Webhook 事件订阅替代轮询，减少调用量。④ 英雄树结构配置化，检查项与节点解耦，规范文档更新后可重新提取；任一数据源不可达时节点标记「数据过期」而非整树不可用。⑤ API 秘钥遵守仓库安全红线：只走环境变量/本地配置，不入库。⑥ 健康度检查流水线与 DocManager 类工具复用同一套文档拉取与 diff 能力。</div>
</div>

<div id="milestones" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:20px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#2563eb;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Milestones</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">里程碑计划</div>
  <div style="font-size:16px;line-height:1.85;color:#64748b;max-width:860px;">自 2026-09-07 启动，按「先打通数据、再出视图、后上健康检查」的顺序推进，2027 年 1 月正式发布。每个里程碑设出口标准，不达标不进入下一阶段。</div>
</div>

| 里程碑 | 时间窗 | 目标 | 出口标准 |
| --- | --- | --- | --- |
| M0 立项与技术验证 | 09-07 ~ 09-18 | 立项评审；TAPD API 打通；iWiki 文档拉通；树图组件选型验证 | 能从一个真实 TAPD 单子与一篇真实规范文档取回数据并渲染 demo 树 |
| M1 数据模型与后端聚合 | 09-21 ~ 10-16 | 英雄树配置模型、进度上卷与 LOQ 判定、TAPD/iWiki 适配器 | 单个英雄全树数据可由服务接口完整输出 |
| M2 前端进度树 MVP | 10-19 ~ 11-13 | 交互式树视图、节点信息卡、TAPD/规范文档跳转 | 目标一达成：一眼看清各职能进度与卡点 |
| M3 资产健康检查 | 11-16 ~ 12-11 | 检查项 AI 提取、规范检查工具、健康度上树 | 目标二达成：技能制作类节点展示红/橙/绿健康度 |
| M4 联调打磨与试运行 | 12-14 ~ 12-31 | 真实英雄数据接入试运行、性能与体验打磨、缺陷清零 | 至少 2 个真实英雄全量接入，连续运行 2 周无 P0/P1 缺陷 |
| M5 正式发布 | 2027-01 上旬 | 发布上线、使用文档与运维交接 | 验收会通过，文档归档 |

<div id="wbs" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:32px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#2563eb;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">WBS</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">任务拆解</div>
  <div style="font-size:16px;line-height:1.85;color:#64748b;max-width:860px;">按里程碑拆解为可独立交付的任务包，一个任务包对应一个 MR 边界，遵守仓库 AGENTS.md 的分支与提交规范。</div>
</div>

| 里程碑 | 任务包 | 交付物 |
| --- | --- | --- |
| M0 | 立项材料与评审 | 本计划书定稿、评审纪要 |
| M0 | TAPD API 验证 | API 账号申请、拉单 demo、网络可达性结论 |
| M0 | iWiki 拉取验证 | 规范文档读取 demo、检查项提取可行性结论 |
| M0 | 前端选型验证 | 树图组件 demo（千级节点渲染与交互验证） |
| M1 | 树结构配置模型 | 英雄树 Schema、七条职能线模板配置 |
| M1 | 进度上卷引擎 | 进度计算 + LOQ 判定单测 |
| M1 | TAPD / iWiki 适配器 | 适配器代码 + 缓存与降级策略 |
| M2 | 树视图前端 | 进度树页面、节点信息卡、外链跳转 |
| M2 | 英雄列表与总览 | 多英雄入口页、整体进度排行 |
| M3 | 检查项提取流水线 | 规范文档 → 检查项清单工具 |
| M3 | 规范检查工具 | 引擎资产检查脚本、健康度评分规则 |
| M3 | 健康度上树 | 节点健康度展示、检查报告详情页 |
| M4 | 试运行接入 | 真实英雄数据接入、看板周报 |
| M4 | 打磨与缺陷清零 | 回归用例、性能优化记录 |
| M5 | 发布与交接 | 使用手册、运维手册、发布公告 |

<div id="research" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:32px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#7c3aed;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Research</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">调研结论与开放问题清单</div>
  <div style="font-size:16px;line-height:1.85;color:#64748b;max-width:860px;">本章区分「已调研闭环」与「待办开放问题」。开放问题均标注缺口、验证方法与闭环节点，执行到对应步骤时按此清单继续深入，闭环后回填结论。</div>
</div>

<div style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;background:#ffffff;border-radius:14px;padding:20px 22px;border:1.5px solid #ddd6fe;margin-bottom:24px;">
  <div style="font-size:15px;font-weight:800;color:#5b21b6;margin-bottom:8px;">已调研闭环（TAPD 方向，2026-09-02）</div>
  <div style="font-size:14px;line-height:1.9;color:#64748b;">鉴权与应用申请流程、任务/需求接口与进度字段（progress 0–100）、状态枚举与工作流状态映射、分页规则（limit≤200）、IDC→OA 三种官方网络方案、Webhook 事件订阅能力——以上均有官方文档依据，可直接作为 M1 适配器开发输入。</div>
</div>

**待办开放问题（按闭环节点排序）**

| # | 开放问题 | 缺口所在 | 待办与验证方法 | 闭环节点 |
| --- | --- | --- | --- | --- |
| R1 | 叶子节点 LOQ 由谁判定 | 方案只定义了父级上卷规则（子级全 L2 父级才 L2），叶子节点的 LOQ 来源未定：人工标记 / 检查工具产出 / TAPD 状态映射 | 立项评审时与方案提出人对齐，产出「叶子节点类型 × LOQ 数据源」对照表 | M0 评审 |
| R2 | TAPD 调用频率限制 | 公开文档未披露 QPS 与日限额 | M0 实测限流阈值；设计兜底：本地缓存 + 按 modified 字段增量拉取 + 错峰调度 | M0 |
| R3 | 部署环境网络可达性 | IDC→OA 受限，服务部署点未定 | M0 在候选部署机用 oss 专用域名方案实测连通性，输出可达性结论 | M0 |
| R4 | 树图前端组件性能 | antv G6 / ECharts tree 均未实测 | M0 出 demo：1000 节点渲染、展开收起、节点点击跳转，记录帧率与内存 | M0 |
| R5 | 引擎资产检查执行载体 | 「生产规范/工程规范」检查项用什么工具执行未定 | 方向：UE Editor Python / Commandlet 批量扫描 uasset 输出结构化报告；M0 用 1 个真实英雄资产跑通 1 条检查项 demo，M3 前定全集 | M0 验证 / M3 定型 |
| R6 | 树节点与 TAPD 单子的关联机制 | 节点配置中如何绑定单子未定义（单任务/多任务/需求+任务树） | M1 树 Schema 设计时定义绑定字段；用真实项目（workspace 20428381）单子验证拉取与字段映射 | M1 |
| R7 | iWiki 程序化读取通道 | 本机 iwiki-cli 已验证可拉取 MD 正文，但平台服务端通道未定 | M1 评估复用 iwiki-cli 同套接口做服务端适配器，确认 token 权限范围与稳定性 | M1 |
| R8 | 检查项 AI 提取准确率 | 未验证，误报会直接污染健康度结论 | M3 前置验证：抽 3 篇规范文档自动提取，人工比对准确率；不达标则检查项以人工维护为主、AI 提取为辅 | M3 前置 |
| R9 | 多英雄数据规模 | 英雄数量、单英雄节点量级未知，影响存储与刷新策略 | M0 统计当前项目英雄清单与职能线节点数，据此定缓存与全量刷新周期 | M0 |

<div id="risks" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:32px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#dc2626;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Risks</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">风险与依赖</div>
</div>

| 风险 / 依赖 | 等级 | 影响 | 应对 |
| --- | --- | --- | --- |
| TAPD API 账号与权限申请周期 | 高 | M0 阻塞 | 启动当周即提申请；先用导出数据做离线 demo 兜底 |
| IDC → OA 网络限制 | 高 | TAPD 数据拉取失败 | 已有三种官方解法（IP+Host 头 / oss 专用域名 / 123 平台），M0 在候选部署机实测选定方案并出可达性结论（开放问题 R3） |
| 检查项 AI 提取准确率不足 | 中 | 健康度误报 | 提取结果人工确认后入库，保留人工维护检查项的通道 |
| 规范文档结构不稳定 | 中 | 提取流水线频繁适配 | 约定规范文档模板；提取失败时节点标记「待维护」 |
| 英雄树配置维护成本 | 中 | 结构变化需改配置 | 结构模板化 + 配置变更走 MR，配版本管理 |
| 引擎资产检查环境依赖 | 中 | M3 阻塞 | 检查工具与平台解耦，先在工程内独立可用再接平台 |

<div id="acceptance" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:32px;margin-bottom:20px;">
  <div style="font-size:14px;font-weight:700;color:#16a34a;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">Acceptance</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">验收标准</div>
</div>

<div style="display:flex;flex-wrap:wrap;gap:16px;margin-bottom:38px;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;">
  <div style="width:calc(50% - 8px);min-width:260px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:22px;border:1.5px solid #bbf7d0;box-shadow:0 6px 24px rgba(22,163,74,0.06);">
    <div style="font-size:18px;font-weight:800;color:#0f172a;margin-bottom:10px;">目标一验收 · 进度可视</div>
    <div style="font-size:15px;line-height:1.9;color:#64748b;">打开任一英雄页面，10 秒内可定位：各职能完成进度、当前 LOQ 阶段、未完成的叶子节点及其负责人与 TAPD 单子链接。</div>
  </div>
  <div style="width:calc(50% - 8px);min-width:260px;box-sizing:border-box;background:#ffffff;border-radius:14px;padding:22px;border:1.5px solid #bbf7d0;box-shadow:0 6px 24px rgba(22,163,74,0.06);">
    <div style="font-size:18px;font-weight:800;color:#0f172a;margin-bottom:10px;">目标二验收 · 资产健康</div>
    <div style="font-size:15px;line-height:1.9;color:#64748b;">资产生产类节点展示健康度（红/橙/绿），点击可查看检查报告：检查项来源（规范文档）、检查结果、失败项明细，且健康度随资产修复在下一次扫描后正确翻转。</div>
  </div>
</div>

<div id="refs" style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB',sans-serif;margin-top:20px;margin-bottom:16px;">
  <div style="font-size:14px;font-weight:700;color:#2563eb;letter-spacing:1.5px;text-transform:uppercase;margin-bottom:10px;">References</div>
  <div style="font-size:34px;font-weight:800;line-height:1.2;letter-spacing:-0.8px;color:#0f172a;margin-bottom:10px;">参考资料</div>
</div>

- [项目英雄进度信息监控平台开发方案（源方案）](https://iwiki.woa.com/p/4037360999)
- [规范检查项示例文档](https://iwiki.woa.com/p/4014926238)
- [TAPD 开放平台 API 文档](https://open.tapd.cn/document/api-doc/API%E6%96%87%E6%A1%A3/api_reference/)
- [项目仓库 Hero_Info_Platform（腾讯工蜂）](https://git.woa.com/oktang/Hero_Info_Platform)
