---
layout: default
title: "Horizon Summary: 2026-11-15 (ZH)"
date: 2026-11-15
lang: zh
---

> 从 39 条内容中筛选出 8 条重要资讯。

---

**科技新闻**
1. [星舰第 15 飞：飞船首次轨道返回后被机械臂捕获](#item-tech-news-1) ⭐️ 8.0/10
2. [Lovable 应用被指因 RLS 不足泄露护照与超 20 万条私信](#item-tech-news-2) ⭐️ 8.0/10
3. [Show HN：约 200 行纯 JAX 实现 DeepSeek V3](#item-tech-news-3) ⭐️ 7.0/10
4. [EFF 警告科技公司再次试图重塑隐私概念](#item-tech-news-4) ⭐️ 7.0/10
5. [Google Project Zero 将按报告后 90 天披露漏洞](#item-tech-news-5) ⭐️ 7.0/10
6. [Cloudflare 开源 AI 代理浏览器 Kitesurf](#item-tech-news-6) ⭐️ 7.0/10
7. [特斯拉 Cybercab 订阅：月费 299 美元，不订阅无法运行](#item-tech-news-7) ⭐️ 7.0/10

**财经新闻**
1. [Anthropic IPO 据报拒绝中国内地及香港投资者下单](#item-finance-news-1) ⭐️ 8.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [星舰第 15 飞：飞船首次轨道返回后被机械臂捕获](https://www.spacex.com/launches/starship-flight-15) ⭐️ 8.0/10

SpaceX 宣布，星舰第 15 次试飞于当地时间 11 月 13 日从得克萨斯州发射，飞船在轨飞行约 22.5 小时、绕地球约 14 圈后返回 Starbase，首次由发射塔机械臂直接捕获，实现轨道级飞船返回后的回收。任务还部署了全部 26 颗星链 V3 卫星，其中 3 颗带摄像头用于检查隔热瓦。超重型助推器未能按计划返回发射塔，因技术问题改在墨西哥湾受控溅落并爆炸，具体原因未公布，因此两级同时回收尚未实现。

hackernews · ls612 · 11月14日 21:22 · [社区讨论](https://news.ycombinator.com/item?id=50500963)

**「背景」** 星舰系统由超重型助推器和飞船两级组成，两级都按可重复使用设计：返回时垂直降落到发射塔旁，由塔上的机械臂夹住承接点，而不是依靠着陆支腿落地或溅落海面。

**「影响与限制」** 对 SpaceX 的星链部署计划而言，本次一次性部署 26 颗 V3 卫星验证了飞船的入轨与卫星释放能力；但复用链条仍缺助推器返场这一环，后续仍需验证双捕获和同一艘飞船复飞，才能判断发射成本能降到什么程度。

**「社区讨论」** 有评论认为星舰相当于修正航天飞机缺陷后的可复用版本，并因流水线生产而更具扩展性，但也有人强调热防护可靠性、同一艘飞船能否复飞以及双捕获能否实现，才决定成本能否真正下降；另有评论认为助推器若多带一些推进剂或许能返场，并将塔臂捕获与南海的缆索式回收方案作对比。这些均为评论者的判断，并非本次任务已验证的结果。

**标签**: `#SpaceX`, `#Starship`, `#reusable rockets`, `#aerospace engineering`, `#spaceflight`

---

<a id="item-tech-news-2"></a>
### [Lovable 应用被指因 RLS 不足泄露护照与超 20 万条私信](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

安全研究团队 Crissy Field 的报告称，部分用 Lovable 构建的应用因 Row-Level Security（RLS）配置不足，暴露了护照信息和超过 20 万条私人消息，受影响的是这些应用的终端用户。Lovable 安全负责人 Igor 回应称，RLS 不足是根因，平台会在应用发布前自动扫描，并向所有用户免费提供更深入的 SAST 扫描；发现问题后，用户可让 Lovable 协助修复，或启用后台自动修复。厂商声明强调发布前的扫描，但未说明对已发布应用的追溯覆盖。

hackernews · armcat · 11月14日 17:43 · [社区讨论](https://news.ycombinator.com/item?id=50499017)

**「背景」** 这些应用依赖 Supabase 的 Postgres 数据库；Supabase 文档说明，Row-Level Security 会在数据库内部执行细粒度授权规则，而暴露 schema 中未启用 RLS 的表，凡拥有相应权限的角色都可读写（tool-2-1）。Supabase 还计划自 2026 年 10 月 30 日起改变 Data API 的默认行为，使现有项目在 public schema 新建的表不再自动通过 REST/GraphQL 暴露，以降低此类默认暴露风险（tool-2-2）。

**「影响」** 对使用 Lovable 构建应用的开发者，RLS 策略就是对外数据边界：一旦某张表允许匿名或公开读取，访问者无需复杂攻击，就能在浏览器网络请求中拿到数据。发布前应逐表核对 RLS，分别用匿名和登录会话做鉴权测试，并运行平台扫描；不能把“页面能打开”当作权限配置正确的证据。

**「社区讨论」** 评论区把部分责任指向 Supabase 的默认配置：有评论称其早年为降低上手门槛而选择了较宽松的默认值，并称虽然相关修复被指已于 10 月 30 日完成，但有报告称既有项目仍沿用旧默认值。另有评论主张平台应采用默认拒绝的数据库、最小权限 API 和自动化鉴权测试，使 AI 生成代码更难形成不安全部署。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://supabase.com/docs/guides/database/postgres/row-level-security">Row Level Security - Supabase Docs</a></li>
<li><a href="https://rlsradar.vercel.app/guides/supabase-data-api-change-oct-30-2026.html">Supabase Oct 30, 2026 Data API change: what it means for RLS</a></li>

</ul>
</details>

**标签**: `#security`, `#AI app builders`, `#Supabase`, `#Row-Level Security`, `#vulnerability disclosure`

---

<a id="item-tech-news-3"></a>
### [Show HN：约 200 行纯 JAX 实现 DeepSeek V3](https://github.com/Vaibhaav-Tiwari/deepseek-v3-jax) ⭐️ 7.0/10

开发者 Vaibhaav Tiwari 在 Hacker News 的 Show HN 发布了用约 200 行纯 JAX 编写的 DeepSeek V3 实现，面向希望从代码层面理解该模型内部结构的工程师。现有材料没有提供源码正文，也未说明它覆盖哪些层、能否加载官方权重、数值是否正确或推理性能如何，因此应将其视为教学性复现展示，而不是官方发布或经基准验证的推理实现。

hackernews · VaibhaavTiwari · 11月14日 15:04 · [社区讨论](https://news.ycombinator.com/item?id=50497589)

**「背景」** DeepSeek V3 采用混合专家（MoE）架构：官方模型卡给出的规模是 671B 总参数，而每个 token 仅激活约 37B 参数。模型容量按总参数计算，单次前向计算只经过其中一部分专家，这是理解此类极简复现的基础。

**「影响」** 对研究 DeepSeek V3 推理内部实现的工程师，这个项目可作为紧凑的逐层阅读参考；但在权重兼容性、数值正确性和性能均未说明的情况下，采用前需要自行验证，不能直接替代官方或生产推理栈。

**「社区讨论」** 多位评论者认为，从第一性原理重建模型是理解推理过程的好方法，也有人询问面向 Java/Python 背景开发者的学习路线。一位使用 RX 7600 XT 16GB 的评论者报告，这是其在 Fedora 与 ROCm 环境中首个端到端跑通的项目，并称至少需要设置 HSA\_OVERRIDE\_GFX\_VERSION=11.0.0，因为 JAX 插件拒绝 gfx1102。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://huggingface.co/deepseek-ai/DeepSeek-V3-Base">deepseek -ai/ DeepSeek - V 3 -Base · Hugging Face</a></li>
<li><a href="https://dev.to/jamilxt/mixture-of-experts-moe-why-big-ai-models-are-cheaper-to-run-than-they-look-2g6i">Mixture of Experts (MoE): Why Big AI Models Are... - DEV Community</a></li>

</ul>
</details>

**标签**: `#JAX`, `#DeepSeek V3`, `#LLM inference`, `#ROCm`, `#minimal implementation`

---

<a id="item-tech-news-4"></a>
### [EFF 警告科技公司再次试图重塑隐私概念](https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again) ⭐️ 7.0/10

电子前沿基金会（EFF）在 11 月 14 日发表的评论文章中警告，科技公司正再次试图重新定义“隐私”概念，而不只是修改某一项数据处理规则。该文引发了对 AI 会议记录工具、无障碍需求和监控规范的讨论；它属于政策倡导分析，不是产品发布或已生效的法规。现有材料仅提供文章摘要，未列出具体公司、版本或政策条款，相关主张仍需回到 EFF 原文核实。

hackernews · gslin · 11月14日 12:45 · [社区讨论](https://news.ycombinator.com/item?id=50496602)

**「背景：环境录音设备先改变了现状」** EFF 的论点建立在此前几年穿戴设备的变化之上：据该文列举，Meta 与 Google 的智能眼镜可以记录佩戴者所见并用 AI 加以描述，Apple 的 Audio Intelligence 功能把 Apple Watch 变成随时转写或总结一天的设备，Amazon 的 Bee 则更进一步，可持续录音并转写（tool-2-1）。这些产品把持续采集音频、视频包装成日常便利，正是 EFF 所指控的“重新定义隐私”的具体对象。


**「社区讨论」** HN 讨论中，有用户描述如今连直接管理者与同事的一对一沟通也会被可见或不可见的 AI 参会者录制并上传，并询问能否把“本次会议无需转录，请关闭 AI 记录器”变成惯例；另一名用户则强调，做得好的实时转录对失聪和重听者可能是变革性的，但本地处理、不保存和不导出仍需产品约束，因为系统离留存只差一个条件分支。还有评论引用《世界人权宣言》第十二条，认为不受任意干涉的隐私权应限制企业通过数据融合获取个人数据。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again">Tech Companies Are Trying to Shift the Entire Concept of ...</a></li>

</ul>
</details>

**标签**: `#privacy`, `#AI surveillance`, `#digital rights`, `#tech policy`, `#AI notetakers`

---

<a id="item-tech-news-5"></a>
### [Google Project Zero 将按报告后 90 天披露漏洞](https://projectzero.google/2026/11/disclosure-policy.html) ⭐️ 7.0/10

Google Project Zero 将把漏洞披露时点设为向厂商报告后 90 天，影响需要在披露前完成修复的软件厂商和开源维护者。讨论中引述的公告称，该团队计划在 2027 年 2 月 2 日把期限缩短至 60 天、2028 年 1 月 3 日缩短至 30 天；在现有材料中未见公告原文，具体适用范围和例外条款尚不清楚。

hackernews · hacb · 11月14日 11:13 · [社区讨论](https://news.ycombinator.com/item?id=50496051)

**「背景：披露期限的含义」** 漏洞披露期限指安全研究团队在通知厂商之后、公开技术细节之前留给对方修复的时间窗口；期限越短，厂商和下游的开源维护者在上游细节公开前完成补丁开发、测试与分发的时间就越少。Project Zero 是 Google 旗下的漏洞研究团队，其披露政策的时间安排会受到厂商与开源项目维护者的密切关注，因为它设定了协调修复的实际节奏。

**「影响」** 对厂商和开源维护者而言，补丁开发、回归测试和发布必须在 90 天窗口内完成；若评论所述时间表属实，2027 年和 2028 年的两次缩短会进一步压缩协调时间，需要提前调整安全响应流程。

**「社区讨论」** 评论中，有人担心 Ubuntu 等发行版需要更长时间才能完成补丁适配，也有人主张立即披露，认为只有外部压力才能促使厂商修复。另有评论提出，发现漏洞的公司应向厂商或开源项目提供同等的产品测试访问，以免披露节奏被用作推广自家产品的杠杆。

**标签**: `#vulnerability disclosure`, `#security policy`, `#Google Project Zero`, `#software maintenance`

---

<a id="item-tech-news-6"></a>
### [Cloudflare 开源 AI 代理浏览器 Kitesurf](https://www.phoronix.com/news/Cloudflare-Kitesurf-Open-Source) ⭐️ 7.0/10

Cloudflare 以 Apache 2.0 协议开源了面向 AI 代理的无状态浏览器 Kitesurf，代码已在 GitHub 发布。该项目基于 Cloudflare Workers 构建，宣称无需浏览器容器即可解析 HTML、处理 CSS 并执行 JavaScript。Cloudflare 还表示，它相比 Chromium 占用更少 CPU 和内存，并能在全球 Workers 网络上按需扩展，但报道未提供基准数据或独立验证。

telegram · zaihuapd · 11月14日 09:33

**「背景」** AI 代理进行网页操作时，通常依赖无头 Chromium，通过 Puppeteer、Playwright 等工具驱动，代价是必须运行并扩展完整的浏览器容器，CPU 与内存开销较高。Cloudflare Kitesurf 的思路是把解析 HTML、处理 CSS 和执行 JavaScript 的能力放到 Cloudflare Workers 这类无服务器运行时上，以无状态方式提供浏览器功能。

**「对代理开发者的影响」** 对构建网页自动化代理的开发者而言，Kitesurf 以 Apache-2.0 开源后可直接审阅代码、在本机运行或部署到 Cloudflare Workers，并提供 CDP 端点，便于现有支持 CDP 的代理客户端和 Chrome DevTools 接入。需注意它仍是实验性引擎，且在 Workers 上为每个页面创建隔离 worker 依赖 Cloudflare Dynamic Workers，这会把相关部署与 Cloudflare 平台绑定。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.cloudflare.com/kitesurf-open-source/">Kitesurf is now open source | Cloudflare Blog</a></li>
<li><a href="https://github.com/cloudflare/kitesurf">GitHub - cloudflare / kitesurf : Kitesurf is an experimental browser ...</a></li>

</ul>
</details>

**标签**: `#ai-agents`, `#open-source`, `#cloudflare-workers`, `#headless-browser`, `#web-automation`

---

<a id="item-tech-news-7"></a>
### [特斯拉 Cybercab 订阅：月费 299 美元，不订阅无法运行](https://www.tesla.com/configurator/api/v4/terms?category=autonomy_subs&amp;amp;locale=en_US&amp;amp;model=cc&amp;amp;saleType=Sale) ⭐️ 7.0/10

特斯拉公布的 Cybercab 自主驾驶订阅协议显示，车辆售价为 29,990 美元，但车主必须每月支付 299 美元订阅费，否则车辆无法运行。特斯拉可提前一个月通知调价；欠费或违规使用可能导致订阅暂停或取消，累计三次警告会停用自动驾驶一周。车辆被限定在指定区域运行，未经授权不得接入网约车、配送或租赁平台。Electrek 指出，Cybercab 与用于 Robotaxi 的 Model Y 使用相同的 AI4 硬件和自动驾驶软件，但面向普通车主的 FSD 仍需人类监督。

telegram · zaihuapd · 11月15日 01:10

**「背景」** Cybercab 属于软件定义汽车：自动驾驶能力由车载 AI4 硬件和软件栈提供，车辆功能可通过订阅条款启用或停用。Electrek 指出，Cybercab 与用于 Robotaxi 的 Model Y 共享 AI4 硬件和相同的自动驾驶软件，但普通车主使用的 FSD 仍需人类监督。

**「影响」** 这意味着购买 Cybercab 的 29,990 美元并不涵盖持续运行能力，车主若停止付费或因违规被停权，车辆将无法按设计运行；有网约车、配送或租赁运营需求者还必须先取得特斯拉授权，不能直接接入商业平台。

**标签**: `#Tesla Cybercab`, `#autonomous vehicles`, `#subscription model`, `#FSD`, `#robotaxi`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [Anthropic IPO 据报拒绝中国内地及香港投资者下单](https://m.economictimes.com/markets/us-stocks/news/anthropic-ipo-share-orders-from-china-are-said-to-be-rebuffed/articleshow/135809948.cms) ⭐️ 8.0/10

据知情人士，Anthropic 的 IPO（首次公开发行）不接受中国内地和香港投资者下单，限制与 ITAR（国际武器贸易条例）出口管制有关。该公司拟以 1.4 万亿美元估值募资至多 904 亿美元，11 月 18 日定价、次日以代码 ANT 上市，认购需求约为可售股份的 6 倍，高盛与摩根士丹利牵头承销。

telegram · zaihuapd · 11月14日 10:18

**「背景」** ITAR（国际武器贸易条例）是美国对国防相关技术出口的管制规则，受控技术不得向特定国家转移；报道将此次拒绝中国内地和香港投资者下单归因于该规则。此前披露的招股信息显示，发行价区间为每股 70 至 78 美元、发行 8.25 亿股，对应约 1.3 万亿美元估值。

**「影响」** 中国内地和香港投资者无法直接下单认购，部分资金转而通过英属维尔京群岛信托、SPV 和掉期结构参与。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.forbes.com/sites/gabrielalinzainescu/2026/11/10/anthropic-ipo-targets-13-trillion-valuation-904-billion-raise/">Anthropic IPO Targets $1.3 Trillion Valuation And A $90 ...</a></li>

</ul>
</details>

**标签**: `#Anthropic IPO`, `#China/Hong Kong investor restrictions`, `#ITAR export controls`, `#AI financing`, `#IPO demand`

---