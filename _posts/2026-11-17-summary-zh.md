---
layout: default
title: "Horizon Summary: 2026-11-17 (ZH)"
date: 2026-11-17
lang: zh
---

> 从 48 条内容中筛选出 15 条重要资讯。

---

**科技新闻**
1. [vLLM v0.34.0 发布：KV 缓存默认扩展，Model Runner V1 移除](#item-tech-news-1) ⭐️ 8.0/10
2. [Jiff 1.0 发布：面向 Rust 的日期时间库](#item-tech-news-2) ⭐️ 8.0/10
3. [Optimizely 被指遭入侵，向 Zoom、GitLab 等站点提供恶意代码](#item-tech-news-3) ⭐️ 8.0/10
4. [美将 AI 芯片出口管制扩至远程访问](#item-tech-news-4) ⭐️ 8.0/10
5. [CMU 推出 CS Learn，免费上线完整学期课程](#item-tech-news-5) ⭐️ 7.0/10
6. [报告称 Windows 11 遥测收集编码代理与开发工具数据](#item-tech-news-6) ⭐️ 7.0/10
7. [Linebender 曲线几何 wiki 的 squircle 条目](#item-tech-news-7) ⭐️ 7.0/10
8. [微软将大规模邮件中断归因于 7 月修复引入的缺陷](#item-tech-news-8) ⭐️ 7.0/10
9. [Marimba：用冻结 Qwen3-ASR 编码器做单次语音查询](#item-tech-news-9) ⭐️ 7.0/10
10. [duetto：不微调，采样时引导预训练音乐 Transformer 实时伴奏爵士](#item-tech-news-10) ⭐️ 7.0/10
11. [美国与九国签署《旧金山宣言》共保超级智能供应链](#item-tech-news-11) ⭐️ 7.0/10
12. [亚马逊称 Artex 驱动 AI 代理窃取 API 密钥支付模型调用](#item-tech-news-12) ⭐️ 7.0/10
13. [阿里、腾讯、月之暗面据报在新模型中收紧网络攻击能力](#item-tech-news-13) ⭐️ 7.0/10

**财经新闻**
1. [卢特尼克因英伟达相关利益冲突质疑面临追问](#item-finance-news-1) ⭐️ 7.0/10
2. [英特尔及 CEO 陈立武遭股东集体诉讼，股价此前暴跌 28.6%](#item-finance-news-2) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0 发布：KV 缓存默认扩展，Model Runner V1 移除](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM v0.34.0 已发布，包含 1,061 次提交和 10 个新模型，其中包括 Mistral Large 4、MiniMax-M3.1-Flash 与 Nemotron-3.5-Transcribe。在 CUDA 和 ROCm 上，可扩展 KV 缓存改为默认启用：缓存按预热及 CUDA 图捕获后的实际空闲显存确定，而不是估算值，默认 gpu\_memory\_utilization 也变为 1.0。该版本移除了 Model Runner V1，V2 成为唯一 GPU runner；默认 --block-size 从 16 改为 64，ROCm 工件仅提供 ROCm 10.0，并要求 huggingface\_hub &gt;= 2.0.0、tokenizers &gt;= 0.23.3 和 timm &gt;= 1.0.30。发布说明列出的性能提升包括 Step5 在 4×GB200 上解码最高 1.95×，以及 GLM-5.3-Flash 输出吞吐达到 1.6×。

github · khluu · 11月16日 23:22

**「背景」** 此前 vLLM 同时并存 Model Runner V1 与 V2 两套 GPU 执行路径，用户在升级时会通过环境变量切换；KV 缓存则按 \`gpu\_memory\_utilization\`（旧默认 0.9）给出的显存占比估算值预分配，而不是按预热后实际剩余显存计算，默认 \`--block-size\` 也是 16。v0.34.0 把这两个默认一并改掉：MRV1 被完全移除，KV 缓存改为按实际空闲显存自适应分配、\`gpu\_memory\_utilization\` 默认 1.0，块大小升到 64，因此保留了旧启动参数或显式设置 \`VLLM\_USE\_V2\_MODEL\_RUNNER=0\` 的部署需要按发布说明逐项调整。

**「影响」** 升级前需逐项检查兼容性：若依赖旧版 KV 缓存估算或块大小 16，可分别传入 --gpu-memory-utilization 0.9（或 --no-enable-extensible-kv-cache）和 --block-size 16 保持原行为；仍使用 VLLM\_USE\_V2\_MODEL\_RUNNER=0、ROCm 7.2 工件、fp\_quant 检查点或 Marlin W4A8 的部署需要迁移或改用新工件。发布说明还提示，新 KV 缓存默认在高并发下可提高吞吐并降低 TTFT，但部分 H200 模型在并发 128 时 TPOT 可能上升 6–18%。

**标签**: `#vLLM`, `#LLM inference`, `#KV cache`, `#release notes`, `#performance`

---

<a id="item-tech-news-2"></a>
### [Jiff 1.0 发布：面向 Rust 的日期时间库](https://burntsushi.net/jiff/) ⭐️ 8.0/10

Jiff 1.0 已作为 Rust 的日期时间库发布，作者是 BurntSushi。Hacker News 上的讨论集中在它的设计、在 Rust 生态中的采用前景，以及对时间尺度的处理。评论中有人提到该库页面谈及 TAI，并追问 UT1 等时间尺度，以及从微秒到百万年、十亿年量级的精度需求。现有材料未给出具体 API、性能或与 chrono 的兼容性细节。

hackernews · burntsushi · 11月16日 16:53 · [社区讨论](https://news.ycombinator.com/item?id=50519744)

**「背景」** Jiff 是 Andrew Gallant（burntsushi）开发的 Rust 日期时间库；其发布记录显示，\`%Q\`/\`%:Q\` 等用于格式化 IANA 时区标识符的说明符早在 0.1 系列就已引入，1.0 是在此前 API 基础上发布的首个主版本。作者在 1.0 导览中把 TAI（国际原子时）等时间标准列为需要明确处理的概念，表明该库除了民用时区和格式化，也涉及时间尺度这一日期时间处理的难点。

**「影响」** 对 Rust 开发者来说，Jiff 1.0 增加了 chrono 之外的一个日期时间库选项，但采用它需要评估迁移成本；chrono 前维护者指出，用户留在 chrono 的重要原因正是其 API 稳定。现有材料没有给出 Jiff 的具体兼容性或时间尺度支持范围，因此迁移前需要自行核实。

**「社区讨论」** chrono 前维护者 quodlibetor 表示，他接手维护是因为认为旧 API 不理想，但改进尝试遭遇阻力，最终因倦怠停止维护，并对 BurntSushi 编写 Jiff 表示感谢；mgrandl 希望 Rust 生态更多采用 Jiff 而非 chrono。Dagonfly 则赞赏项目明确说明 Jiff 并非适用于所有场景，另有评论者追问 TAI、UT1 等时间尺度的处理方式。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://burntsushi.net/jiff/">A datetime library for Rust - Andrew Gallant&#x27;s Blog</a></li>
<li><a href="https://github.com/BurntSushi/jiff/releases">Releases · BurntSushi / jiff · GitHub</a></li>

</ul>
</details>

**标签**: `#Rust`, `#datetime`, `#libraries`, `#open source`, `#software engineering`

---

<a id="item-tech-news-3"></a>
### [Optimizely 被指遭入侵，向 Zoom、GitLab 等站点提供恶意代码](https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/) ⭐️ 8.0/10

据一篇报道，Optimizely 被指遭入侵，并通过使用其脚本的客户网站向访问者提供恶意代码，涉及 Zoom、GitLab 等站点。报道将其归为第三方 Web 脚本和供应商供应链风险；对嵌入 Optimizely 的站点来说，非预期代码可能在自身页面环境中执行。攻击者如何取得跨客户项目的写入权限、受影响站点与访问者的完整范围，目前仍未得到说明。

hackernews · kristjansson · 11月16日 23:00 · [社区讨论](https://news.ycombinator.com/item?id=50524767)

**「背景：第三方脚本的信任边界」** 许多网站会把 Optimizely 这类第三方优化与实验脚本直接嵌入页面，由供应商的 CDN 下发并在访客浏览器中执行；因此，一旦该供应商的代码分发被攻破，所有嵌入其代码的站点都会同时暴露。评论区提到的 Google Tag Manager 也属于同一模式：它让市场团队无需工程介入就能往页面加“标签”，代价是每篇文章都会加载大量第三方 JavaScript。

**「受影响方的后续处置」** 据后续报道，Optimizely 表示已控制该事件、封堵了被利用的路径、清除了注入代码，并直接联系了受影响客户；报道称共涉及 178 个组织、188 个被感染的 Optimizely JavaScript 文件。对使用 Web Experimentation 的站点而言，实际后果是需自行核查页面是否仍加载异常脚本，并重新评估第三方脚本的加载与审批方式，而不是假定供应商修复后即完全无恙。

**「社区讨论」** 评论者把矛头指向第三方标签和脚本的权限过大：有人以 Google Tag Manager 为例，称营销团队可绕过工程直接加脚本，造成页面脚本膨胀；也有人认为 Optimizely 与大型站点缺少冷却期、分阶段发布和自动安全检查，应承担后果。另有评论者追问，若涉事大型站点并不处理加密货币或支付，恶意脚本为何能造成所述影响，认为原报道缺少这一环。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://cybersecuritynews.com/optimizely-websites-hijacked/">Hackers Infect 178 Major Websites via Optimizely to Steal ...</a></li>
<li><a href="https://osintsights.com/optimizely-supply-chain-compromised-malware-hits-major-sites">Optimizely Supply Chain Compromised, Malware Hits Major Sites</a></li>

</ul>
</details>

**标签**: `#supply chain security`, `#third-party scripts`, `#web security`, `#Optimizely`, `#malware`

---

<a id="item-tech-news-4"></a>
### [美将 AI 芯片出口管制扩至远程访问](https://www.reuters.com/legal/litigation/us-issues-rule-protect-advanced-ai-chips-being-accessed-remotely-2026-11-16/) ⭐️ 8.0/10

美国商务部于 11 月 16 日发布临时最终规则，将先进 AI 芯片和服务器的出口管制扩大到远程访问，以阻止通过第三国数据中心规避限制。路透社报道称，该规则由财政部和国家安全委员会主导起草，可能进一步收紧中国获取先进芯片的渠道；The Verge 还报道，向印度尼西亚、马来西亚、新加坡、泰国和巴西再出口 AI 芯片需申请许可。现有报道未披露许可的具体判定标准或生效日期。

telegram · zaihuapd · 11月16日 14:44

**「背景」** 美国工业与安全局（BIS）的出口管制此前主要针对先进芯片和服务器的实体出口与再出口，第三国数据中心通过远程方式调用算力并不在同等许可框架内。此次临时最终规则把远程访问纳入管制，正是为了封堵这条既有路径。

**「合规影响」** 在新加坡、马来西亚、印度尼西亚、泰国和巴西再出口先进 AI 芯片的企业，现在需要先取得许可证；提供第三国数据中心远程访问的云服务商和运营商也需核查客户与用途，以免构成向中国实体提供受控算力。相关数据中心和转口安排可能因此延迟或需要调整。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://wccftech.com/the-u-s-shuts-chinas-access-to-advanced-chips-via-singapore-brazil-indonesia-malaysia-and-thailand-as-scott-bessent-gives-nvidia-10-days-to-show-it-did-not-goose-its-revenues/">The U . S . Shuts China&#x27;s Access To Advanced Chips Via Singapore ...</a></li>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-16/us-moves-to-limit-remote-access-to-advanced-ai-chips">US Moves to Curb China’s Remote Access to Nvidia’s AI Chips</a></li>
<li><a href="https://qz.com/us-ai-chip-reexport-licenses-five-countries-111626">U . S . is requiring licenses to reexport AI chips to five countries</a></li>

</ul>
</details>

**标签**: `#AI chip export controls`, `#US semiconductor policy`, `#remote access`, `#data centers`, `#AI hardware`

---

<a id="item-tech-news-5"></a>
### [CMU 推出 CS Learn，免费上线完整学期课程](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

卡内基梅隆大学推出 CS Learn，开始在 YouTube 免费发布该校当前计算机科学课程完整学期的讲座视频。项目负责人 Phillip Compeau 在评论中表示，本周每天首播一门课程，明年 1 月还会上线更多课程；部分学生开发了自动化制作工具，让小团队也能完成发布。已披露的信息集中在讲座视频，课程覆盖多个 CS 方向，评论中提到的例子包括机器学习系统和概率与计算，但作业、项目或反馈是否配套尚未说明。

hackernews · pcompeau · 11月16日 20:43 · [社区讨论](https://news.ycombinator.com/item?id=50522980)

**「背景」** 这一做法有先例：MIT OpenCourseWare 长期免费公开其大量本科与研究生课程材料，目标是覆盖“几乎全部”课程内容。CMU 的 CS Learn 同样以免费开放课程为核心，但强调发布当前课程的整学期讲座，并用学生开发的工具自动化制作流程。

**「影响」** 自学者和学生可以免费按学期进度观看 CMU 当前 CS 课程的讲座，但若缺少配套作业、项目和反馈，这种资源更接近公开旁听，完整课程体验仍取决于后续材料。

**「社区讨论」** 评论者总体欢迎这一资源，CMU 校友点名期待 Tianqi Chen 的机器学习系统课程，并请求增加分布式系统、操作系统和统计学等课程；也有人提醒，若只有讲座而缺少项目与反馈，学习效果会打折扣。另有评论认为，扎实掌握基础才能把 AI 当作增强工具，否则更可能被它替代。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/MIT_OpenCourseWare">MIT OpenCourseWare - Wikipedia</a></li>
<li><a href="https://ocw.mit.edu/">MIT OpenCourseWare | Free Online Course Materials</a></li>

</ul>
</details>

**标签**: `#computer science education`, `#open courseware`, `#CMU`, `#machine learning systems`, `#YouTube`

---

<a id="item-tech-news-6"></a>
### [报告称 Windows 11 遥测收集编码代理与开发工具数据](https://xusheng.dev/posts/windows-coding-agent-telemetry/) ⭐️ 7.0/10

一篇开发者博文称，Windows 11 会记录用户使用哪些编码代理和开发工具，并在启用“可选诊断数据”时上传这些信息，而该选项默认开启。受影响的是在 Windows 11 上使用这类工具的开发者；文章给出的关闭路径为“设置 → 隐私和安全性 → 诊断和反馈”。现有材料未包含微软的说明或具体字段清单，因此收集范围和上传内容仍应以官方文档核实为准。

hackernews · cwaffles · 11月16日 22:58 · [社区讨论](https://news.ycombinator.com/item?id=50524736)

**「背景」** Windows 11 的“可选诊断数据”是诊断反馈中的一个层级，开启后会向微软发送额外的使用信息。此次结论来自对 MissionControlAggregator 的逆向分析：它记录的是开发工具是否运行过的位图，而非提示词或会话内容，并且只有在启用可选诊断数据时才会上传。

**「实际影响」** 对在 Windows 上本地运行编码代理的开发者来说，直接后果是隔离能力取决于代理是否接入微软的 MXC（Microsoft Execution Containers）：微软文档称 MXC 可限制 AI 生成命令对文件、凭据和网络的访问，而 Claude Code 的适配请求在 6 月仍以 GitHub 议题形式存在。未接入时，团队仍可能依赖 Docker 等外部隔离手段来约束代理执行。

**「社区讨论」** 评论对这类遥测是否合理看法不一：有评论者认为它有助于微软确定开发优先级，并提到 Windows 的 AI 代理沙箱 MXC 才在 10 月 7 日推出、Claude Code 尚未支持；也有人指出显卡驱动和浏览器等同样会收集类似信息，并给出关闭诊断数据的路径。另有用户报告称，单机游戏在 Linux 上大多运行良好，但多人游戏仍有兼容问题，并把迁移到 Linux 视为可行选择。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://xusheng.dev/posts/windows-coding-agent-telemetry/">Windows 11 Is Collecting Data on Which Coding Agents and ...</a></li>
<li><a href="https://windowsforum.com/news/windows-11-optional-telemetry-can-report-coding-agent-usage-research-finds.452631/">Windows 11 Optional Telemetry Can Report Coding Agent Usage ...</a></li>
<li><a href="https://news.lavx.hu/article/windows-11-collects-data-on-coding-agents-and-developer-tools-you-use">Windows 11 Collects Data on Coding Agents and Developer Tools ...</a></li>
<li><a href="https://github.com/anthropics/claude-code/issues/69495">Support Microsoft MXC sandboxing · Issue #69495 · anthropics ...</a></li>
<li><a href="https://learn.microsoft.com/en-us/windows/apps/develop/mxc/">Microsoft Execution Containers overview - Windows apps</a></li>

</ul>
</details>

**标签**: `#Windows 11`, `#telemetry`, `#privacy`, `#developer tools`, `#AI coding agents`

---

<a id="item-tech-news-7"></a>
### [Linebender 曲线几何 wiki 的 squircle 条目](https://linebender.org/wiki/curves/squircle/) ⭐️ 7.0/10

Linebender 的曲线几何 wiki 提供了一篇关于 squircle（介于方形与圆形之间的圆角形状）的技术条目，面向图形渲染和 UI 设计工程师。该页面是参考性资料，重点在 squircle 及相关曲线几何，而不是新库、版本或兼容性发布。对需要选择圆角形状表示或理解相关曲线术语的读者，它可作为几何背景的入口。

hackernews · raphlinus · 11月16日 07:55 · [社区讨论](https://news.ycombinator.com/item?id=50515151)

**「背景」** Squircle（方圆形）指介于正方形与圆形之间的圆角形状，常用于图标和界面元素的轮廓设计，也是曲线连续性讨论中的典型例子。发布该文的 Linebender 是一个关注 2D 图形与用户界面设计、主要用 Rust 开发项目的社区。

**「影响」** 希望在产品中使用 squircle 的团队不能把这篇 wiki 当作现成实现；它更适合作为几何概念参考，实际落地仍要自行选择曲线表示并接入渲染管线。

**「社区讨论」** 评论中，darthcircuit 以 Zune 第二代播放器的方向键为例，称其 squircle 手感顺滑；thot\_experiment 则分享了一个仍处于探索阶段的样条、超椭圆与回旋曲线创作工具演示。另有评论者强调，避免导数不连续正是这类曲线在需要与物理现实交互时变得有趣的原因。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://linebender.org/">Homepage for the Linebender organization</a></li>

</ul>
</details>

**标签**: `#computer graphics`, `#UI design`, `#geometry`, `#curves`, `#splines`

---

<a id="item-tech-news-8"></a>
### [微软将大规模邮件中断归因于 7 月修复引入的缺陷](https://www.theregister.com/saas/2026/11/16/microsoft-blames-monster-email-outage-on-software-defect-introduced-in-july-fix/5310026) ⭐️ 7.0/10

微软将一次大规模邮件中断归因于今年 7 月一次修复所引入的软件缺陷。这一说法来自对故障的复盘，指向前一次变更留下的回归问题，而非孤立的新故障。

hackernews · Bender · 11月16日 13:18 · [社区讨论](https://news.ycombinator.com/item?id=50517321)

**「事件背景」** 2026 年 11 月 12 日（周四），Outlook 发生大规模中断，数百万用户和机构受影响超过 12 小时；直到周五，微软才报告取得“边际成功”。11 月 16 日的事故报告将根因指向一项为 Microsoft 365 网络网关服务器准备、自 7 月起全球部署的修复，该改动运行三个多月后才暴露出软件缺陷。

**「实际影响」** 对依赖 Outlook 的机构而言，直接后果是业务邮件在数小时内不可用：报道显示医院、学校、企业和美国国会办公室均受影响，Downdetector 记录到的受影响用户分布在 70 多个国家，连微软员工也无法使用邮件。邮件仍是这些机构的关键业务通道，中断期间只能转向其他通信方式维持运转。

**「社区讨论」** 评论者把恢复过程类比为电网的“黑启动”，强调必须先卸掉负载、再按顺序恢复，否则可能再次压垮系统；也有人质疑为何不通过限流或分批放行连接来降低负载。另有评论对关键网络基础设施使用 Windows 感到意外，并指出低端测试环境通过了 7 月代码，却未暴露生产环境中的并发缺陷。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.npr.org/2026/11/12/nx-s1-6039343/outlook-down-widespread-outage-microsoft-email">A negative Outlook: Microsoft scrambles to fix email outage : NPR</a></li>
<li><a href="https://cybersecuritynews.com/microsoft-outage-incident-report/">Microsoft Reveals How a Hidden Windows Bug Took Down Microsoft ...</a></li>
<li><a href="https://www.npr.org/2026/11/12/nx-s1-6039343/outlook-down-widespread-outage-microsoft-email">A negative Outlook: Microsoft scrambles to fix email outage : NPR</a></li>
<li><a href="https://www.nytimes.com/2026/11/13/business/microsoft-outage.html">Inside Microsoft ’s Rush to Get Back Online After a Global Outage</a></li>

</ul>
</details>

**标签**: `#Microsoft`, `#email outage`, `#incident postmortem`, `#site reliability`, `#software defect`

---

<a id="item-tech-news-9"></a>
### [Marimba：用冻结 Qwen3-ASR 编码器做单次语音查询](https://www.reddit.com/r/MachineLearning/comments/1xxsqro/marimba_a_system_one_model_for_speech_r/) ⭐️ 7.0/10

Reddit 用户 /u/solanotodesch 发布了 arXiv 预印本 2611.18330，介绍 Marimba：用户针对一段音频窗口提出文字问题（是/否、多选或打分），系统返回经过校准的概率。每个 8 秒窗口只运行一次冻结的 Qwen3-ASR-0.6B 编码器，所有问题共用这次前向计算；术语检测（如“有没有说 satellite”）是零样本的，用解码器的贪心结果和 4 条 beam 假设打分，再做 Platt 校准；语种识别直接使用 ASR 模型自带的语言分数；话轮结束读取冻结的第 18 层，说话人变化与人数读取第 12 层。作者称在 1000 条公开问题上，9 项测试中有 6 项与 Qwen3-Omni（30B-A3B）持平或更优，但在 Speech Commands 上落后；语种识别在 300 条 FLEURS 片段上达到 100%，说话人变化 AUROC 为 0.966–0.980（AMI、VoxConverse），高于 ECAPA，人数估计优于 pyannote 3.1。作者同时承认两项限制：话轮结束读数是在 Smart Turn 数据上训练的，因此该行结果只是同分布表现（在 Smart Turn 自己的测试集上 AUROC 为 0.930，低于 Smart Turn v3.2 的 0.982；在 ICSI 会议上为 0.716 对 0.712，基本持平），并且模型不泛化到未见任务，在 CochlScene 场景分类上所有预测头都处于随机水平。代码与 Apache-2.0 权重已公开，可用 pip install marimba-audio 安装；上述基准均为作者自报，尚未经独立验证。

reddit · r/MachineLearning · /u/solanotodesch · 11月16日 15:47

**「背景」** 语音识别模型通常只被用来做转写，但其编码器输出只是音频的一段表示，可以为其他判别式任务复用。Marimba 的做法是将 Qwen3-ASR-0.6B 编码器冻结，每 8 秒音频窗口只做一次前向计算，再针对不同查询接上小型读出层，或对解码器生成的假设重新打分并做 Platt 校准，从而避免为每个任务单独微调模型。

**「影响」** 对需要在音频窗口上做固定几类判定（术语是否出现、语种、话轮结束、说话人变化与人数）的开发者来说，这条路线意味着用一个 0.6B 冻结编码器的单次前向加若干轻量预测头，替代为每个问题调用 30B 级 omni 模型。代价是覆盖面被锁死：每个新查询类型都要在冻结层特征上另训预测头并另行校准，作者自己的 CochlScene 实验显示未训练的任务直接掉到随机水平；话轮结束检测也不宜直接替换 Smart Turn v3.2，因为作者报告在其测试集上仍落后（0.930 对 0.982）。

**标签**: `#speech recognition`, `#audio models`, `#efficient inference`, `#model calibration`, `#Qwen3-ASR`

---

<a id="item-tech-news-10"></a>
### [duetto：不微调，采样时引导预训练音乐 Transformer 实时伴奏爵士](https://www.reddit.com/r/MachineLearning/comments/1xxkyh3/steering_a_pretrained_music_transformer_at/) ⭐️ 7.0/10

单作者项目 duetto 展示了一个面向 MIDI 键盘的实时爵士伴奏系统：它把演奏者的音符与模型输出放进同一事件序列，逐音生成独奏、伴奏和行走贝斯，并在演奏者停止时接手独奏。其做法是不微调预训练的 Anticipatory Music Transformer（Thickstun 等，2023），而是在每次采样前用规则层编辑 logits：屏蔽不允许的音（如等待中的声部、超出音域、非正拍贝斯音），并抬高当前和弦音、强拍引导音或引用乐句下一音的权重。乐句取自 Weimar Jazz Database 的转录独奏，按独奏者换气处切分、移调到曲目和弦上并在一个副歌内发展；作者称演示（Autumn Leaves，160 bpm）中约 61% 的独奏音符来自引用乐句或主题。服务器提前采样约 1 秒音乐，并在演奏者落键时重采样尚未播放的部分；作者报告 3080 Ti 上每音约 12 ms（medium）和 18 ms（large），Jetson Orin Nano 上 large 约 90 ms/音，仍足以现场演奏；代码免费用于非商业用途，但作者也指出系统会偏离演奏者、响应难以预测，且规则与模型创意的平衡很脆弱，且未报告独立评估。

reddit · r/MachineLearning · /u/GGAllin43 · 11月16日 09:19

**「模型背景」** Duetto 依赖的 Anticipatory Music Transformer 是 Thickstun 等人于 2023 年发布的自回归音乐模型，其训练目标包含 infilling，因此能够根据已有旋律生成伴奏；论文报告在 20 秒片段的人工评估中，其伴奏音乐性与人类创作相近。该模型以音符事件序列为输入并逐事件续写，这使 duetto 可以在不微调预训练模型的情况下，于采样阶段施加外部规则。

**「影响」** 对做实时符号音乐生成的开发者，duetto 提供了一个可运行的非商业代码基线：控制逻辑可以在采样时用规则层迭代，而不必先承担微调成本。作者报告的漂移、不可预测响应和规则权重脆弱，意味着采用者需要把规则调参与重采样策略当作主要工程工作，而不是把它当作可直接依赖的成品伴奏。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/abs/2306.08620">[2306.08620] Anticipatory Music Transformer - arXiv.org</a></li>
<li><a href="https://crfm.stanford.edu/2023/06/16/anticipatory-music-transformer.html">Anticipatory Music Transformer: A Controllable Infilling ...</a></li>

</ul>
</details>

**标签**: `#music-generation`, `#transformer`, `#inference-time-steering`, `#real-time-music`, `#pretrained-models`

---

<a id="item-tech-news-11"></a>
### [美国与九国签署《旧金山宣言》共保超级智能供应链](https://www.state.gov/releases/office-of-the-spokesman/2026/11/the-san-francisco-declaration-on-the-secure-foundations-of-enduring-prosperity/) ⭐️ 7.0/10

11 月 15 日，美国与澳大利亚、印度、以色列、日本、韩国、卡塔尔、新加坡、阿联酋和英国签署《旧金山宣言》，确认经济安全是国家安全根基，并将共同保护支撑超级智能（SI）供应链的敏感技术和关键基础设施。宣言提出设立五个工作组，分别负责创新政策框架、SI 在关键领域应用、SI 全栈供应链协作、安全港与供应链安全枢纽，以及 SI 安全与韧性。现有信息只说明了签署方和工作组分工，尚未给出约束性承诺、执行时间表或具体技术标准。

telegram · zaihuapd · 11月16日 10:40

**「背景」** 《旧金山宣言》在 Pax Silica Founders Retreat 上签署，该活动由美国负责经济事务的副国务卿 Jacob Helberg 主持。据公开资料，这一框架旨在降低在关键矿产、AI 模型和半导体芯片等环节对美国对手的依赖，因此参与国需要先就应保护的敏感技术和基础设施形成共同基线。

**「影响」** 这一安排把 SI 全栈供应链的安全协作放到政府间工作组层面；在签署国运营的 AI 芯片、云服务和关键基础设施企业需要关注后续工作组是否出台供应链审查、安全港或认证要求。现有信息尚未列出具体合规义务、资金安排或时间表。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/San_Francisco_Declaration_on_the_Secure_Foundations_of_Enduring_Prosperity">San Francisco Declaration on the Secure Foundations of Enduring Prosperity</a></li>
<li><a href="https://www.investing.com/news/world-news/us-nine-nations-sign-san-francisco-declaration-on-ai-security-5028448">U.S., nine nations sign San Francisco declaration on AI security By...</a></li>

</ul>
</details>

**标签**: `#AI policy`, `#AI supply chain`, `#international agreement`, `#AI governance`, `#critical infrastructure`

---

<a id="item-tech-news-12"></a>
### [亚马逊称 Artex 驱动 AI 代理窃取 API 密钥支付模型调用](https://cybernews.com/security/amazon-autonomous-cybercrime-artex-framework/) ⭐️ 7.0/10

亚马逊称，攻击者利用开源渗透测试框架 Artex 驱动 AI 代理，窃取 LiteLLM、Dify 等公网暴露 AI 应用的 API 密钥，并在验证后汇入共享池，用于支付更多大模型调用。亚马逊表示，这轮活动从 10 月 3 日持续到 11 月 5 日，最终被其诱饵网络 MadPot 截获并阻断。亚马逊以中等信心将行动归因于一个与中国相关的威胁组织，同时指出并非所有被列目标都已失陷，并已通知可能受影响的 AWS 客户。

telegram · zaihuapd · 11月16日 13:00

**「背景」** 这类攻击的前提是：LiteLLM、One API、Dify、FastGPT、Langflow、Open WebUI 等 LLM 网关与应用构建工具通常把接入各家模型厂商所用的 API 密钥保存在实例配置中，一旦这些实例直接暴露在公网，密钥就可能被读取。据 The Hacker News 和 Quartz 援引的智能体自身记录，这些代理会逐个扫描上述产品，并按一份将各产品对应到已知入口的“作战手册”行动，亚马逊的 MadPot 诱饵网络正是在这一过程中截获了相关活动。

**「影响」** 对运行 LiteLLM、Dify 等公网暴露 AI 应用的组织而言，具体风险是 API 密钥被他人验证、集中并用于产生额外模型调用费用；亚马逊称已通知可能受影响的 AWS 客户，相关客户需要检查密钥暴露情况与异常调用记录。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://thehackernews.com/2026/11/amazon-uncovers-ai-agent-campaign.html">Amazon Uncovers AI Agent Campaign Targeting LiteLLM , Dify , and...</a></li>
<li><a href="https://qz.com/amazon-ai-agents-steal-provider-keys-artex-111626">Amazon captured records of AI agents trying to steal AI keys</a></li>

</ul>
</details>

**标签**: `#AI security`, `#autonomous agents`, `#API key theft`, `#cybercrime`, `#AWS`

---

<a id="item-tech-news-13"></a>
### [阿里、腾讯、月之暗面据报在新模型中收紧网络攻击能力](https://www.bloomberg.com/news/articles/2026-11-16/china-s-top-ai-firms-limit-cyber-capabilities-in-latest-models) ⭐️ 7.0/10

据彭博报道，阿里巴巴、腾讯、月之暗面等中国头部 AI 公司在新一代模型中削弱了进攻性网络攻击能力，同时提升了防御性网络安全表现。阿里最新旗舰 Qwen 未以开放权重形式发布，用户无法下载并自定义完整版本。腾讯在发布 Hy4 之前已削减了模型的网络功能。上述调整与商务部上月公布的出口管制草案相关，该草案拟禁止可攻击关键基础设施和政府网络的 AI 工具出口。

telegram · zaihuapd · 11月17日 02:20

**「背景」** 中国商务部上月公布的出口管制草案拟禁止出口可用于攻击关键基础设施和政府网络的 AI 工具，这是报道中多家中国 AI 公司调整新模型网络能力的政策背景。开放权重意味着模型参数可供下载、在本地部署或微调；报道特别指出，阿里最新旗舰 Qwen 未采用这一发布方式，用户无法下载并自定义完整版本。

**「影响」** 对依靠开放权重进行微调或本地部署的开发者而言，旗舰 Qwen 不再提供完整下载意味着只能改用厂商提供的接口，或继续使用此前的开放版本；若出口管制草案按现有文本落地，向关键基础设施和政府网络提供攻击性 AI 工具的渠道将受到直接限制。

**标签**: `#AI policy`, `#cybersecurity`, `#open-weight models`, `#China AI`, `#export controls`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [卢特尼克因英伟达相关利益冲突质疑面临追问](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

CNBC 报道，美国商务部长霍华德·卢特尼克因其子执掌的坎托·菲茨杰拉德公司与英伟达的密切关系面临利益冲突质疑。据 CNBC 对证券申报文件的分析，该公司申报持有的英伟达股票数量在 2025 年 9 月至 2026 年 3 月间下降 49%，从约 350 万股（市值 6.52 亿美元）降至 178 万股（市值 3.10 亿美元）；同期，据 Axios 报道，卢特尼克多次抵制对涉嫌将英伟达芯片走私至中国的新加坡公司 Megaspeed 采取行动。报道称，目前没有证据表明卢特尼克泄露非公开信息，也没有证据显示其子事先知情或持股变化与上述警告有关。

rss · CNBC Finance · 11月16日 12:14

**「背景」** 霍华德·卢特尼克原为华尔街投行坎托·菲茨杰拉德（Cantor Fitzgerald）的首席执行官，于 2025 年 2 月出任美国商务部长；商务部负责出口管制，包括将涉嫌违规的外国企业列入实体清单（即限制交易名单）。坎托目前由他的儿子布兰登和凯尔领导，这层政商关系是外界审视该公司与英伟达往来时的制度背景。

**「影响」** 据 CNN 报道，黄仁勋本周已辞去英伟达首席执行官一职；与此同时，据 CNBC 报道，美国商务部正针对中国数据中心用途的出口漏洞采取措施，这意味着原本经由新加坡等中转渠道流向中国的 AI 芯片路径及相关云服务合作方，可能面临更严格的出口许可审查。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.businessinsider.com/howard-lutnick-billionaire-donald-trumps-commerce-secretary-nominee-cantor-fitzgerald-2024-11">Meet Howard Lutnick , Donald Trump&#x27;s Nominee for Commerce ...</a></li>
<li><a href="https://edition.cnn.com/2026/11/16/tech/nvidia-sex-spies-serious-problems">Lies, spies and sex are just one part of the Nvidia story.</a></li>
<li><a href="https://www.cnbc.com/2026/11/16/nvidia-commerce-china-lutnick.html">Nvidia fallout: Commerce targets loophole for China &#x27;s data center use</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#US-China export controls`, `#conflict of interest`, `#Commerce Department`, `#corporate governance`

---

<a id="item-finance-news-2"></a>
### [英特尔及 CEO 陈立武遭股东集体诉讼，股价此前暴跌 28.6%](https://www.investing.com/news/stock-market-news/intel-sued-by-shareholders-following-29-stock-plunge-5028171) ⭐️ 7.0/10

英特尔及其 CEO 陈立武、CFO 津斯纳被股东提起集体诉讼，股东指控公司隐瞒个人电脑（PC）需求疲软和库存积压的影响；诉讼涉及 2026 年 7 月 23 日至 10 月 29 日买入股票的投资者。此前公司于 10 月 29 日发布的第四季度营收和利润预测不及预期，次日股价下跌 28.6%，市值蒸发约 1400 亿美元。

telegram · zaihuapd · 11月16日 11:10

**「背景」** 这起拟议的股东集体诉讼依据美国 1934 年《证券交易法》提起，覆盖 2026 年 7 月 23 日至 10 月 29 日买入英特尔股票的投资者，允许股东就涉嫌虚假陈述或隐瞒重大信息向公司及高管索赔。

**「影响」** 这起诉讼寻求代表在 2026 年 7 月 23 日至 10 月 29 日买入的投资者，相关股东可能被纳入集体索赔，英特尔则面临辩护成本和潜在赔偿。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://finance.yahoo.com/markets/stocks/articles/why-intel-facing-shareholder-lawsuit-143331644.html?fr=sycsrp_catchall">Why Is Intel Facing a Shareholder Lawsuit Over Its PC Slowdown?</a></li>

</ul>
</details>

**标签**: `#Intel`, `#shareholder lawsuit`, `#semiconductor`, `#stock plunge`, `#earnings warning`

---