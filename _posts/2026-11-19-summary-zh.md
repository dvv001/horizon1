---
layout: default
title: "Horizon Summary: 2026-11-19 (ZH)"
date: 2026-11-19
lang: zh
---

> 从 44 条内容中筛选出 13 条重要资讯。

---

**科技新闻**
1. [谷歌发布 Gemini 4 Neon，主打编程智能体与低价调用](#item-tech-news-1) ⭐️ 8.0/10
2. [Nginx HTTP/2 被曝未认证远程代码执行漏洞](#item-tech-news-2) ⭐️ 8.0/10
3. [微软 Ignite 2026 发布七款新模型，主打可扩展性价比](#item-tech-news-3) ⭐️ 7.0/10
4. [Google DeepMind 上线 Genie 4，仅限符合条件的 AI Ultra 订阅者](#item-tech-news-4) ⭐️ 7.0/10
5. [Quad9 退出法国：DNS 不该充当反盗版执法点](#item-tech-news-5) ⭐️ 7.0/10
6. [从 4004 到 486：一篇 x86 早期处理器技术史](#item-tech-news-6) ⭐️ 7.0/10
7. [把旅行者 1 号拆到单颗存储芯片的互动网站](#item-tech-news-7) ⭐️ 7.0/10

**财经新闻**
1. [美联储会议纪要：多数官员认为仍需进一步加息](#item-finance-news-1) ⭐️ 8.0/10
2. [腾讯三季度营收增长 8%，AI 资本开支升至 814 亿元](#item-finance-news-2) ⭐️ 8.0/10
3. [美联储理事沃勒称或需在 12 月加息 50 个基点](#item-finance-news-3) ⭐️ 7.0/10
4. [特朗普抵达深圳出席亚太经合组织领导人非正式会议](#item-finance-news-4) ⭐️ 7.0/10
5. [中韩宣布自贸协定服务与投资后续谈判实质性结束](#item-finance-news-5) ⭐️ 7.0/10
6. [九部门拟要求新能源汽车&quot;车电一体报废&quot;](#item-finance-news-6) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [谷歌发布 Gemini 4 Neon，主打编程智能体与低价调用](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/) ⭐️ 8.0/10

谷歌发布 Gemini 4 Neon，面向复杂软件工程、知识工作与科研工作流，已向开发者、企业客户以及 Google AI Pro/Ultra 订阅用户开放。该模型支持 100 万 token 上下文，定价为每百万输入 token 3 美元、缓存输入 0.15 美元、输出 15 美元。谷歌方面给出的评测数据显示，它在 Artificial Analysis 编程智能体指数上以 58.6 分登顶，在智能指数 xhigh 档以 61 分排在总榜第三，Terminal-Bench 4.1 得分为 65.2%，默认 high 档下单任务成本比 Carbon 低 32%。上述基准均为厂商及第三方指数口径，尚缺少独立复现的验证。

hackernews · yigitdemirag · 11月18日 21:34 · [社区讨论](https://news.ycombinator.com/item?id=50552424)

**「背景」** Google 的 Gemini 4 系列此前已有 Carbon 型号；Hacker News 评论指出，Carbon 仍被定位为面向长程任务的模型，而 Neon 与它并行，主打更快的端到端执行和编程代理工作流。这有助于理解 Google 这次并非用单一旗舰取代旧型号，而是在同一代中按任务类型拆分定位。

**「成本影响」** 对使用 Neon 运行编程智能体的团队来说，成本控制的关键在于输出规模，单价并非主要因素：Artificial Analysis 测得该模型在智能指数评测中生成 2.83 亿 token，远高于 6510 万 token 的中位数；按每百万输出 token 15 美元计算，长输出会迅速放大账单。开发者应设置输出上限，并利用缓存输入 0.15 美元/百万 token 的折扣；在批量任务前，还应按实际工作负载复核成本。

**「社区讨论」** Hacker News 评论的主要抱怨集中在命名上：多位用户表示难以把 Neon、Carbon、Sol、Opus 等新名称对应到具体使用场景，并追问谷歌命名规则中是否体现“模型尺寸级别”。关于产品定位，有评论指出 Neon 总分虽高于 Carbon，但 Carbon 仍被定位为“长周期”模型，其在 CritPt 等研究级推理评测上得分更高；也有人提到 OpenRouter 上 Neon 的生成速度约为每秒 127 token、明显快于 Carbon 的每秒 46 token，并对旗舰型号反而更快感到困惑。另有用户凭主观体验认为 Neon 在基准上接近 Anthropic 的 Opus 5.5，但整体通用智能感仍不及后者。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://artificialanalysis.ai/models/gemini-4-neon">Gemini 4 Neon: Intelligence, Performance &amp; Price Analysis</a></li>
<li><a href="https://deepmind.google/blog/introducing-gemini-4-neon/">Introducing Gemini 4 Neon - deepmind.google</a></li>

</ul>
</details>

**标签**: `#Gemini 4 Neon`, `#Google AI`, `#large language models`, `#model releases`, `#AI benchmarking`

---

<a id="item-tech-news-2"></a>
### [Nginx HTTP/2 被曝未认证远程代码执行漏洞](https://www.wiz.io/blog/nginx-http2-rce-vulnerabilities) ⭐️ 8.0/10

Xint 公开了名为 NGINX2Root 的攻击链：将 5 个 Nginx 漏洞与 1 个 Linux 内核缺陷串联后，攻击者可从 Nginx 访客权限获取主机 root；其中 CVE-2026-123007 是 HTTP/2 流控内存破坏漏洞，未认证即可在 worker 进程中执行命令。Nginx 1.30.7 和 1.31.9 已于 11 月 18 日修复 10 个 CVE。Rapid7 已发布 PoC，目前没有在野利用报告；无法升级的用户应关闭对外 HTTP/2。

hackernews · speedping · 11月18日 15:19 · [社区讨论](https://news.ycombinator.com/item?id=50547374)

**「背景：HTTP/2 流控与内存破坏」** HTTP/2 通过流量控制窗口限制单个流可发送的数据量，接收方用 WINDOW\_UPDATE 帧调整窗口；如果实现没有校验窗口上限，攻击者就能构造请求让窗口超出允许阈值，进而写坏堆内存。按 Red Hat 与 NVD 的漏洞描述，这就是 CVE-2026-123007：未认证攻击者可借堆缓冲区溢出实现任意代码执行或拒绝服务，最典型的表现是 nginx worker 进程发生段错误。该缺陷影响启用了 HTTP/2 的 NGINX Plus 与开源版配置，修复版本为 nginx 1.31.9 和 1.30.7。

**「影响与处置」** 对启用 HTTP/2 的 Nginx 实例，直接处置方式是升级到 1.30.7 或 1.31.9；如果无法升级，就应关闭对外的 HTTP/2 监听。未启用 HTTP/2 的部署不会受到这条攻击路径影响。Rapid7 已发布 PoC，公网可访问且能接收大流量 HTTP/2 连接的服务应优先排查；不过社区讨论指出，利用需要约 128GB 流量和特定 CPU 指令，因此实际门槛高于普通未认证 RCE。

**「社区讨论」** 评论者对实际风险存在分歧：有人指出 HTTP/2 并非 Nginx 默认启用、仅约 12% 的服务器使用，并称利用需要约 128Gb 的 HTTP/2 流量和特定 CPU 指令，因此认为影响有限。也有评论批评相关修复提交提前约一周出现在开源仓库，且未及时发布“关闭 HTTP/2”的公告，可能给监控仓库的攻击者留下窗口。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://cycode.com/blog/nginx2root-cve-2026-123007/">NGINX2Root (CVE-2026-123007): Affected Versions, How to Check ...</a></li>
<li><a href="https://access.redhat.com/security/cve/cve-2026-123007">CVE-2026-123007 - Red Hat Customer Portal</a></li>
<li><a href="https://nvd.nist.gov/vuln/detail/cve-2026-123007">NVD-CVE-2026-123007</a></li>

</ul>
</details>

**标签**: `#nginx`, `#http2`, `#vulnerability`, `#remote-code-execution`, `#security`

---

<a id="item-tech-news-3"></a>
### [微软 Ignite 2026 发布七款新模型，主打可扩展性价比](https://microsoft.ai/news/microsoft-ignite-2026/) ⭐️ 7.0/10

微软在 Ignite 2026 大会上发布了七款新 AI 模型，官方将其定位为“可扩展的性价比”（scalable price-performance）。讨论中被具体点名的模型是 MAI Code 2；但现有材料只到发布公告层面，没有给出参数规模、基准测试分数、许可证类型或具体上线时间，因此这批模型的实际能力与定价目前无法独立核实。围绕这次发布，讨论主要集中于微软能否在价格与性能上与 Anthropic、OpenAI 的同级模型正面竞争。

hackernews · gmays · 11月18日 16:08 · [社区讨论](https://news.ycombinator.com/item?id=50548021)

**「背景」** 微软在 Ignite 2026 上公布七款模型，其中 MAI Code 2 属于其自研 MAI 系列，已有社区成员表示将其用于日常编码测试。素材没有给出这些模型的参数、许可证或基准数据，因此“可扩展的性价比”目前仍是厂商表述，需独立评测确认。

**「对成本敏感团队的直接影响」** 对用量大的团队来说，微软给出的比价依据是：MAI Image 2.7 在 Artificial Analysis 图像编辑榜单位列第一，价格仅为 GPT Image 2.6 Sunburst 的五分之一；MAI Image 2.7 Flash 则面向高并发的图像生成场景。因此，高吞吐的图像编辑与转写工作负载就有了重新核算成本的理由。对于开发团队，微软将 MAI Code 2 定位为与 Opus、Sol 同级的 agentic 编码模型，卖点集中在“可规模化”的价格；但公告与主题演讲均未提及开放权重，只强调“Your weights”式的定制，所以在选型前需要确认调用方式和迁移成本。

**「社区讨论」** 一位评论者称自己已在日常工作中实测 MAI Code 2，认为“相当好用”，对微软把它与 Opus 或 Sol 放在同一水平的说法“不会有太多异议”。另一位评论者则主张，微软若想争到市场份额，就应把部分模型开源或开放权重，否则会重演 Windows Phone 的结局；也有评论借 Anthropic 定价偏高看空其 IPO，并质疑 Ignite 主题演讲缺乏实质内容——这些都是个人观点，既不构成对模型能力的验证，也不代表社区共识。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://microsoft.ai/news/microsoft-ignite-2026/">Seven new world-class models at scalable price-performance ...</a></li>
<li><a href="https://microsoft.ai/news/microsoft-ignite-2026-mai-keynote/">Microsoft Ignite 2026: MAI keynote transcript | Microsoft AI</a></li>

</ul>
</details>

**标签**: `#Microsoft`, `#AI models`, `#price-performance`, `#MAI Code 2`, `#model competition`

---

<a id="item-tech-news-4"></a>
### [Google DeepMind 上线 Genie 4，仅限符合条件的 AI Ultra 订阅者](https://blog.google/innovation-and-ai/models-and-research/google-deepmind/genie-4-now-available-project-genie/) ⭐️ 7.0/10

Google DeepMind 于 11 月 18 日宣布 Genie 4 可供使用。据公告中被引用的措辞，其开放对象是“符合条件的 Google AI Ultra 订阅者”（Eligible Google AI Ultra subscribers），并非所有用户，但现有材料未说明具体资格条件、地区范围与定价。所给页面正文为空，因此 Genie 4 相对前代的具体能力提升、模型规格与调用方式均无法核实。

hackernews · leumon · 11月18日 18:49 · [社区讨论](https://news.ycombinator.com/item?id=50550415)

**「背景」** Project Genie 是 Google DeepMind 提供世界模型体验的产品入口；Genie 4 是该入口的新一代模型，接替此前的 Genie 3。现有对照信息显示，Genie 4 相比 Genie 3 增加了可编辑世界和音频等能力，因此这次变化属于同一产品线的模型升级。

**「实际影响」** 对希望使用的订阅者和开发者来说，当前最直接的障碍是资格判定而非技术本身：一位评论者称其 Workspace 账户无法开通 Ultra，换用个人 Gmail 后 Ultra 页面仍只显示 Genie 3，因此无法判断这是英国地区限制（此前某代 Genie 曾仅限美国）还是页面尚未更新。潜在用户需要先确认账户类型与所在地区是否在支持范围内，再考虑付费。

**「社区讨论」** 讨论主要围绕付费与可得性：有长期用户抱怨 Google 始终说不清用户到底怎样才能付费使用其产品；另有评论者批评相关讨论几乎只关注定价与能力，很少涉及这类技术可能带来的负面后果，并称自己对这类发布“一样都不想要”。也有评论者对 DeepMind 的工作表示欣赏，认为其动机更像是出于对技术的热爱，并畅想世界模型未来或可作为游戏引擎使用。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.google/innovation-and-ai/models-and-research/google-deepmind/genie-4-now-available-project-genie/">Project Genie update featuring Genie 4 - The Keyword</a></li>
<li><a href="https://www.online-tech-tips.com/google-genie-4-access-ai-ultra/">Google opens Genie 4 access to eligible AI Ultra subscribers</a></li>

</ul>
</details>

**标签**: `#Genie 4`, `#Google DeepMind`, `#world models`, `#generative AI`, `#product launch`

---

<a id="item-tech-news-5"></a>
### [Quad9 退出法国：DNS 不该充当反盗版执法点](https://techstackups.com/articles/quad9-leaves-france-dns-blocking/) ⭐️ 7.0/10

这篇评论文章以 Quad9 退出法国为例，主张 DNS 解析器不应成为反盗版屏蔽的执行点。文章把法国方面的 DNS 阻断要求放进隐私、审查和互联网基础设施治理的框架中，认为让中立解析器承担版权执法会扩大言论过滤的风险。文章属于政策论证，而非技术发布。

hackernews · ritzaco · 11月18日 13:18 · [社区讨论](https://news.ycombinator.com/item?id=50545958)

**「背景」** DNS 解析器负责把域名映射到 IP 地址；一旦解析器被要求按封锁令拒绝解析某些域名，受影响的不只是被指侵权的站点，而是所有依赖该解析器的用户。Tech Stackups 的梳理称，Quad9 选择在 2026 年 11 月 24 日停止为法国用户服务，而不执行 beIN Sports 获得的封锁令；Cloudflare 则把这一退出视为强制 DNS 层面封锁的风险案例。

**「影响」** 对法国用户和隐私工具而言，Quad9 的退出意味着少了一个独立公共解析器选项；文章据此提醒，若 DNS 层被当作版权执法关口，其他中立解析器也可能面临同样的合规或退出压力。

**「社区讨论」** 评论者中，trentnix 认为不以起诉盗版者为核心的反盗版措施只是压制言论的后门；bemtevi 则主张用更好的正版体验竞争，并抱怨合法观看电影仍需订阅或买 DVD。AppalachianEng 质疑在 AI 公司已大量使用版权内容的情况下继续针对个人，skrebbel 则追问应把责任归于误判的法院还是荒谬的立法。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.cloudflare.com/quad9-withdrawal-from-france/">Quad 9 ’s withdrawal from France : A canary in the... | Cloudflare Blog</a></li>
<li><a href="https://techstackups.com/articles/quad9-leaves-france-dns-blocking/">Quad 9 Is Leaving France : Why DNS Resolvers Are... | Tech Stackups</a></li>

</ul>
</details>

**标签**: `#DNS`, `#internet censorship`, `#privacy`, `#piracy policy`, `#internet infrastructure`

---

<a id="item-tech-news-6"></a>
### [从 4004 到 486：一篇 x86 早期处理器技术史](https://pikuma.com/blog/history-of-x86-4004-to-486) ⭐️ 7.0/10

pikuma 博客发布了一篇长文，按时间顺序梳理 Intel 从 4004 经 8008、8080、8085 到 8086/8088、80286、80386 直至 486 的早期处理器谱系，重点讲架构层面的演变，而非产品年表。文章在 Hacker News 上引来多位读者补充与纠错：有人指出小端序最初是为了加快 2200 的数据访问速度、而非便于算术，算术上的好处要到 8080 支持 16 位运算才显现；有人指出 8085 的地址/数据复用总线在 8008 和 8080 上同样存在，并非 8085 独有。针对文中加粗的“Intel 没有设计 8008 指令集”一说，读者认为方向大体正确，但 Intel 工程师（包括 Stan Mazor）确实对其做了增补，例如加入递增和递减指令。另有读者强调，4004 与 8008 除人员重叠外并无直接继承关系。

hackernews · ibobev · 11月18日 14:47 · [社区讨论](https://news.ycombinator.com/item?id=50546967)

**「背景」** Intel 4004 于 1971 年作为该公司首款商用微处理器问世，原本面向计算器等嵌入式用途；Intel 随后另开一条 8 位产品线，其中 8008 于 1972 年 4 月推出，采用面向字节的设计和 14 位外部地址总线，最多可寻址 16KB 内存。此后 8080、8086 以及 286、386、486 逐代扩展指令集与地址空间，构成这篇文章所梳理的 x86 谱系。

**「社区讨论」** 评论者多为亲历者与考据型读者：jgord 回忆自己在 8088、Hercules 单显卡上从 GW-BASIC 到 A86 汇编再到 Turbo Pascal 的学习经历，并称 80386 的 32 位线性地址模型才让桌面端“严肃计算”成为可能。较具技术价值的分歧集中在细节归属上——小端序的原始动因、地址/数据复用总线的适用范围、8008 指令集究竟由谁设计，评论者均以具体芯片和总线行为为依据提出修正。skissane 则质疑 Intel 与 AMD 为何仍让现代 PC 以 16 位实模式启动，认为改为直接进入长模式或 32 位保护模式只会影响 BIOS 编写者。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.tomshardware.com/picturestory/710-history-of-intel-cpus.html">The History Of Intel CPUs: Updated! | Tom&#x27;s Hardware</a></li>
<li><a href="https://cpumuseum.jimdofree.com/museum/intel/8008/">Intel 8008 - CPU MUSEUM - MUSEUM OF MICROPROCESSORS...</a></li>
<li><a href="https://www.eie.polyu.edu.hk/~enyhchan/cpu.pdf">Evolution of Intel Microprocessors 1971 to 2007.PDF</a></li>

</ul>
</details>

**标签**: `#x86 history`, `#CPU architecture`, `#Intel microprocessors`, `#computer history`, `#retrocomputing`

---

<a id="item-tech-news-7"></a>
### [把旅行者 1 号拆到单颗存储芯片的互动网站](https://rshekhar.com/voyager/) ⭐️ 7.0/10

作者 raj-shekhar 在 Show HN 发布了一个已上线的互动网站，可把旅行者 1 号硬件逐层展开到数据计算机中的单颗存储芯片，并查看核电池内的 24 个钚球、金唱片封套说明以及当年通过无线电修复探测器的过程。站点还展示两艘旅行者号当前的位置和正在接收信号的地球天线。作者称，旅行者 1 号当天距地球达到一光日；这属于发布者的说法，站点本身是科普可视化，而非新的工程进展。

hackernews · raj-shekhar · 11月18日 16:18 · [社区讨论](https://news.ycombinator.com/item?id=50548161)

**「背景」** 旅行者 1 号的飞行计算机用上世纪七十年代制造的 CMOS 存储芯片保存指令与数据，这些芯片没有为全部内容提供冗余，一旦某个存储单元读值出错，地面只能通过无线电重新安排代码位置来绕过故障。由于探测器当时已距地球约一光日，单程信号需要约一天，修复过程必须依靠逐条指令上行并在两天后才知道结果。这个交互站点正是把这类子系统按舱段、存储平面一直到单个比特的层级组织起来，供人逐层查看。

**「社区讨论」** 有评论者称赞可视化效果，并分享了自己的金唱片致敬页面和把原始音频解码成图像的独立项目。也有人追问站点是否主要由 AI 生成、是否经过权威资料核对，以及 CMOS 存储芯片究竟因何种物理机制持续读错。

**标签**: `#Voyager 1`, `#interactive visualization`, `#spacecraft computers`, `#hardware history`, `#memory chips`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [美联储会议纪要：多数官员认为仍需进一步加息](https://www.cnbc.com/2026/11/18/fed-minutes-october-2026.html) ⭐️ 8.0/10

美联储 10 月会议纪要显示，几乎所有与会官员都判断，为使通胀及时回到 2%的目标，进一步上调联邦基金利率目标区间很可能仍是合适的；但本次会议最终以 10 票赞成、2 票反对，决定将基准利率维持在 3.75%-4%不变。

rss · CNBC Finance · 11月18日 19:41

**「背景」** 美联储在 9 月实施了 2023 年以来的首次加息，把基准利率区间上调至 3.75%-4%，因此 10 月会议选择按兵不动、等待更多数据（tool-1-1）。

**「影响」** 如果 AI 投资回报不及预期，持有相关债务的投资者和金融机构可能承受被放大的损失：美联储工作人员指出，这些债务大量通过资产负债表外的租赁承诺和循环融资安排形成，风险敞口还越来越集中在少数几家公司手中。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.cnbc.com/2026/09/16/fed-rate-decision-september-2026.html">Fed rate decision September 2026 : Rates rise to 3.75%-4%</a></li>
<li><a href="https://decision-intel.shapingtomorrow.com/scans/ai-automation/2026-05-30-ai-offbalance-financing/scan.html">Off the Books: How AI &#x27;s Build-Out Quietly Became a Financing Risk ...</a></li>
<li><a href="https://www.federalreserve.gov/monetarypolicy/files/fomcminutes20261028.pdf">Minutes of the Federal Open Market Committee - October 27-28, 2026</a></li>

</ul>
</details>

**标签**: `#Federal Reserve`, `#monetary policy`, `#inflation`, `#interest rates`, `#AI financial risk`

---

<a id="item-finance-news-2"></a>
### [腾讯三季度营收增长 8%，AI 资本开支升至 814 亿元](https://api3.cls.cn/share/article/2537922?os=android&amp;amp;sv=8.8.5&amp;amp;app=cailianpress&amp;amp;selected=) ⭐️ 8.0/10

腾讯公布 2026 年第三季度财报：营收 2073 亿元，同比增长 8%，低于市场预期；归母净利润 636 亿元，同比增长 0.8%。当季资本开支为 814.33 亿元，远超市场预估的 554 亿元，单季自由现金流为负 691 亿元；腾讯还称，WorkBuddy 日均 Token 用量超过 100 万亿，为国内大语言模型产品最高。

telegram · zaihuapd · 11月18日 09:20

**「背景」** WorkBuddy 是腾讯面向办公场景推出的桌面 AI 智能体（AI agent），可自动拆解任务并生成报告、表格等成品；Token 则是衡量大模型处理文本量的计量单位。

**「影响」** 腾讯本季经营活动产生的现金净额仅 26 亿元，远不足以覆盖 651 亿元的资本开支付款，缺口主要由账上现金填补；这意味着其 AI 算力投入正直接消耗公司自有资金，并转化为算力与云基础设施供应商的订单。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.workbuddy.ai/">WorkBuddy - AI Agent for Everyday Office Work</a></li>
<li><a href="https://www.developersdigest.tech/blog/tencent-workbuddy-explained-pricing-free-models-2026">Tencent WorkBuddy Explained: Pricing, Free Models, Verdict</a></li>
<li><a href="https://www.tencent.com/wp-content/uploads/2026/11/Tencent-Announces-2026-Third-Quarter-Results.pdf">For Immediate Release - Tencent</a></li>
<li><a href="https://cryptobriefing.com/tencent-negative-free-cash-flow-q3-ai/">Tencent reports negative free cash flow of RMB69.1 billion in ...</a></li>

</ul>
</details>

**标签**: `#Tencent`, `#earnings`, `#AI capex`, `#free cash flow`, `#China tech`

---

<a id="item-finance-news-3"></a>
### [美联储理事沃勒称或需在 12 月加息 50 个基点](https://www.cnbc.com/2026/11/18/federal-reserve-governor-christopher-waller.html) ⭐️ 7.0/10

美联储理事克里斯托弗·沃勒 11 月 18 日表示，可能需要“震动”人们，在 12 月 8 日至 9 日的会议上加息 0.5 个百分点（50 个基点），并称要逆转 2025 年的三次 25 个基点降息，甚至可能加得更多。这只是一名官员的建议，并非美联储已作出的决定；芝商所 FedWatch 显示，市场期货目前完全定价 12 月加息 25 个基点。

rss · CNBC Finance · 11月18日 15:13

**「背景」** 美联储的通胀目标是 2%，但多数近期通胀读数高于 3%；2025 年美联储曾因担忧劳动力市场而降息三次，今年 2 月底美国与以色列对伊朗的打击推高能源价格，关税影响也仍在。

**标签**: `#Federal Reserve`, `#monetary policy`, `#interest rates`, `#inflation`

---

<a id="item-finance-news-4"></a>
### [特朗普抵达深圳出席亚太经合组织领导人非正式会议](https://weibo.com/1699432410/5366644789744407) ⭐️ 7.0/10

据新华社和央视新闻报道，美国总统特朗普乘专机抵达深圳宝安国际机场，国家主席习近平前往迎接。特朗普将出席于 11 月 18 日至 19 日举行的亚太经合组织第三十三次领导人非正式会议。

telegram · zaihuapd · 11月18日 08:42

**「背景」** 亚太经合组织是亚太经济体讨论贸易与经济合作的论坛；据九号台报道，本届第 33 次领导人非正式会议由中国主办，于 11 月 18 日至 19 日举行。

**「潜在影响」** 此次会晤可能检验美中能否在关税与出口管制上取得进展，从而影响依赖双边贸易的制造商和出口商。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.nine.com.au/world-news/donald-trump-arrives-in-china-for-xi-jinping-vladimir-putin-apec-summit-20261118-p61fex.html">APEC Summit: Albanese poses alongside Putin at... | Nine.com.au</a></li>
<li><a href="https://fortune.com/2026/11/18/trump-xi-putin-shenzhen-apec-trade-truce-export-controls/">What&#x27;s at stake for Trump and Xi in Shenzhen: A trade truce ...</a></li>

</ul>
</details>

**标签**: `#US-China relations`, `#APEC`, `#summit diplomacy`, `#trade policy`

---

<a id="item-finance-news-5"></a>
### [中韩宣布自贸协定服务与投资后续谈判实质性结束](https://x.com/Jaemyung_Lee/status/2122988472994791476) ⭐️ 7.0/10

中韩双方 11 月 18 日宣布，自贸协定服务与投资后续谈判已实质性结束；中方承诺在电影、游戏等领域给予韩国最惠国待遇（即不低于对其他贸易伙伴的待遇），并扩大旅游、法律、建筑和金融等领域开放。双方还同意将视听节目共同制作范围从电影扩大至电视剧、动画、综艺和纪录片，但部分技术事项仍需在工作层面继续协商。

telegram · zaihuapd · 11月18日 10:02

**「背景」** 中韩自贸协定的服务与投资后续谈判于 2018 年 3 月启动；据韩方报道，这是该领域谈判八年来首次取得进展。此次双方宣布的是“实质性结束”，部分技术事项仍留待工作层面协商完成。

**「影响」** 若相关安排最终生效，韩国影视、游戏以及旅游、法律、建筑、金融等服务企业将获得更宽的对华市场准入，合拍范围扩大也将直接影响相关制作公司。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.chosun.com/english/national-en/2026/11/19/NTPG5ZDJMBAKLH427BSO5LHJKU/">Korea-China FTA Service, Investment Negotiations ...</a></li>

</ul>
</details>

**标签**: `#China-South Korea FTA`, `#services and investment`, `#trade policy`, `#cultural industries`, `#market access`

---

<a id="item-finance-news-6"></a>
### [九部门拟要求新能源汽车&quot;车电一体报废&quot;](https://wallstreetcn.com/articles/3786200) ⭐️ 7.0/10

商务部等九部门于 11 月 17 日提出修订《报废机动车回收管理办法实施细则》，拟推动新能源汽车&quot;车电一体报废&quot;回收拆解，并研究制定动力电池数字身份证管理制度及相关行政法规。该修订仍属提议，具体管理办法尚待制定。

telegram · zaihuapd · 11月18日 12:22

**「背景」** 今年 4 月施行的暂行办法已规定，报废新能源汽车缺失动力电池的，应认定为车辆缺失；此次拟议修订是在此基础上，进一步明确回收环节要求并记录电池流转信息。

**标签**: `#新能源汽车`, `#动力电池回收`, `#报废汽车回收`, `#政策监管`, `#电池数字身份证`

---