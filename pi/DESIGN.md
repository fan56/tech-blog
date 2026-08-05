# 「我的 Pi Agent」展示页 — 设计文档 v1

## 0. 目标

单文件自包含 HTML(无 CDN、无外部库,离线可用),介绍 fliu56 的 pi agent:
默认能力(pi v0.83 原生)+ 个人增强(85 skills / 20 agents / ~20 extensions / 4 MCP)

+ 一张**动画架构图**,分类生动讲解每一块。深色科技感。

## 1. 设计 Token(来自已装前端 skill 规范的综合)

+ 底色 #050505;层 #0D0F14 / #11141B;主文 #F4F5F7;次 #9AA1AC;弱 #5B6270
+ 描边 rgba(255,255,255,.08~.12);**单一强调色 青绿 #22D3EE**(只用于连接线/状态/高亮,禁紫、禁渐变文字)
+ 字体栈(系统字体,自包含):标题/英文数字 `Space Grotesk`→回退 `-apple-system`;正文 `-apple-system, "PingFang SC", "Noto Sans SC"`;节点/代码/标签 `ui-monospace, "SF Mono", monospace`
+ H1 clamp(3rem,5vw,5.5rem) ≤2行;H2 4xl~5xl;正文 15-16px、max-w-65ch、行高 1.7
+ 圆角全局统一 16px;卡片用 **Double-Bezel 双层**(外 p-1.5 ring-white/10 rounded-2xl + 内芯 inset 高光)
+ 动效只动 transform/opacity;入场 fade-up 600-800ms、ease [0.16,1,0.3,1]、stagger 80-100ms;节点 hover scale-1.05/700ms;全部 IntersectionObserver + `prefers-reduced-motion` 降级

## 2. 页面结构(7 段)

1. **Hero** — 无 stats/无 logo 墙/无假终端。H1「Pi · 我的终端 AI 编排者」+ 副文案(pi 极简内核 + 我用扩展物塑形的工作流)+ 一个 CTA(锚点跳架构图)。
2. **架构图(核心)** — 4 层垂直堆叠(核心引擎 → 扩展层 → 智能体/技能层 → 外部接入),SVG 连接线随滚动 scrub 绘制,每层节点 stagger 入场。见 §3。
3. **默认 vs 增强** — 左右对比:pi 原生极简(7 工具/4 类扩展物/会话树/自动压缩)vs 我的叠加(85 skills/20 agents/4 MCP/Volvo 业务栈)。不做等大三卡。
4. **能力归类(核心内容)** — 5 类,不等宽 bento(grid-flow-dense,数学互锁,无空 cell):
   + 设计与审美:anti-ui-slop、design-taste-frontend、high-end-visual-design、gpt-taste、brandkit、imagegen-* 等(24 个通用技能)
   + 飞书办公自动化:lark 全家桶 22 个(IM/文档/多维表格/日历/邮箱/妙记/审批/白板/会议)
   + 车云业务工程:cs-geely/vcc-*、cicd-fullchain/quick、k8s-troubleshoot、kafka、vault、VIN 扫描、friction 报表
   + 工程效能:lean-ctx、pi-lens、agent-browser、markitdown、cmux、tavily
   + 智能体团队:workhorse 牛马狗、oldfox 老法师、rpiv 流水线 20 个角色
5. **Agent 团队特写** — 牛马狗(干活主力,workhorse-gate 限权)/ 老法师(把关,GLM5.2 max 思考)/ 编排者身份(APPEND_SYSTEM:研究必派 sub-agent、无审核不标完成)。带一句话工作流「分析→派遣→验证→汇总」。
6. **配置快照** — 默认模型 deepseek-v4-flash(思考 high)、主题 high-contrast-dark(51 token 可热重载)、AGENTS.md 七条铁律(编号列表,非 emoji)、双 skill 库路径、cron 监控任务。
7. **Footer** — 极简一行:pi v0.83 · MIT · 单文件 HTML。

## 3. 架构图规格(重点)

布局:4 个横向 band(从上到下 Core → Extensions → Agents & Skills → External),band 之间用 SVG 曲线连接线(虚线 dash,滚动 scrub 时 stroke-dashoffset 从 0 画到 1,回退为入场即画完)。

+ **Band A 核心引擎(1 个主节点 + 4 子节点)**:主节点「pi engine v0.83」;子:内置工具×7 / 会话树与分支 / 上下文自动压缩 / 30+ 模型路由(7 档思考)
+ **Band B 扩展层(2 组)**:Extensions ~20 个(pi-lens/pi-dcp/pi-goal/pi-subagents/rpiv-*…);MCP ×4(lean-ctx / codebase-memory / chrome-devtools / anysearch)
+ **Band C 智能体与技能(2 组)**:Agent 团队 20 个(牛马狗/老法师/工作流角色);Skills 85 个(通用设计 24 + 业务工作流 61)
+ **Band D 外部接入(1 组)**:Volvo 业务( GitLab CI / K8s / Artifactory / Vault / Kafka / Redis / PG / 飞书 )+ cmux/ghostty

节点 = 真实 mini-UI(小终端窗/小卡片带真实名称),禁 div 假终端、禁假版本号、禁 emoji。节点 hover:内描边青绿 + scale 1.05。主节点常亮青色呼吸(仅 transform/opacity)。

## 4. 文案基调

中文为主,英文术语保留。不用 em-dash、不用「·」堆砌、不用 buzzword、不用「Not X. Y.」腔调。每段 ≤4 行。数字全部真实(85/20/4/11 等,来源:实际盘点)。

## 5. 验收清单

+ 单文件、无外部依赖、离线可开
+ prefers-reduced-motion 生效
+ 手机(<768px)单列、w-full、px-4 py-8
+ 架构图滚动绘制 + 节点交互正常
+ 无紫渐变/无 #000/无 emoji/无假终端/无 marquee/无 bounce
