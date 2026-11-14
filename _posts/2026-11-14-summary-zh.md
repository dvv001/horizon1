---
layout: default
title: "Horizon Summary: 2026-11-14 (ZH)"
date: 2026-11-14
lang: zh
---

> 从 39 条内容中筛选出 7 条重要资讯。

---

**科技新闻**
1. [TorchTitan 在 384 块 GH200 上训练 1T MoE](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI 推出 ChatGPT Wallet，支持令牌化卡支付](#item-tech-news-2) ⭐️ 8.0/10
3. [Python 早期贡献者 Tim Peters 去世，享年 74 岁](#item-tech-news-3) ⭐️ 7.0/10
4. [微软 Outlook、Teams 与 Copilot 全球中断逾 12 小时](#item-tech-news-4) ⭐️ 7.0/10
5. [DeepSeek 开放应用 API，集成搜索、文件与语音能力](#item-tech-news-5) ⭐️ 7.0/10

**财经新闻**
1. [CNBC：卢特尼克之子执掌的坎托减持英伟达，引发利益冲突质疑](#item-finance-news-1) ⭐️ 8.0/10
2. [芝加哥联储主席古尔斯比：美联储在通胀上“肯定还有工作要做”](#item-finance-news-2) ⭐️ 8.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [TorchTitan 在 384 块 GH200 上训练 1T MoE](https://www.reddit.com/r/MachineLearning/comments/1xvce5h/scaling_to_1t_moe_on_torchtitan_p/) ⭐️ 8.0/10

一篇 Reddit 工程帖称，团队在 JUPITER 的 384 块 GH200 上用 TorchTitan 训练约 1T 参数 MoE，采用 384 路 FSDP 加节点内 4 路专家并行，达到约 1,300 tokens/s/GPU，较起点提升 14 倍。帖子称其跳过流水线并行以缩短单步时间，并通过全量激活重计算、把检查点激活卸载到 Grace、用 Muon 替代 Adam，把序列长度推到 64k。作者还报告了按注意力开销分桶以缓解慢节点（最差 rank 从平均的 7.9 倍降到 1.15 倍，吞吐 +13%）、用 bf16 全对全替代 fp32 reduce-scatter，以及把 Newton-Schulz 放到 GPU 上执行使优化器步骤从 42 秒降到约 2 秒、吞吐 +35%。这些是作者自述、汇总 Domyn 与 PyTorch 博客的社区报告，并非同行评审或独立复现。

reddit · r/MachineLearning · /u/f14-bertolotti · 11月13日 16:28

**「背景」** PyTorch 博客的配套文章称，同一项目在 JUPITER 上训练的是 951.9B 参数的 MoE：每个副本使用 384 块 NVIDIA GH200（96 个节点），并可扩展到 4 个副本、共 1,536 块 GPU；吞吐从 90 提升到约 1,300 tokens/s/GPU。该文还提到 FlexShard 参数放置和 Muon 优化器等手段，这些正是 Reddit 作者所总结的 TorchTitan 训练栈中的已有组件。

**「影响」** 对在 GH200 等 InfiniBand 集群上使用 FSDP 的团队，一个直接可操作点是：若显存仍有 25–30 GiB 空闲却在约 70% HBM 利用率触发分配器重试，应检查 FSDP 集合通信的临时缓冲区是否落在侧流；作者称改用 FSDP2 的 unshard\_async\_op（正转为公开 API）并提前释放梯度后，384 个 rank 的重试归零、峰值保留显存降 13.5 GiB、吞吐 +21%。这一结果目前仍属该团队自报，迁移前需在自己的负载上验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://pytorch.org/blog/training-a-1t-parameter-moe-on-eu-public-infrastructure-with-pytorch-and-torchtitan/">Training a 1T-Parameter MoE on EU public ... - PyTorch</a></li>
<li><a href="https://daily.dev/posts/training-a-1t-parameter-moe-on-eu-public-infrastructure-with-pytorch-and-torchtitan-tjfwzdwty">Training a 1T-Parameter MoE on EU public infrastructure...</a></li>

</ul>
</details>

**标签**: `#MoE`, `#distributed training`, `#TorchTitan`, `#PyTorch`, `#GH200`

---

<a id="item-tech-news-2"></a>
### [OpenAI 推出 ChatGPT Wallet，支持令牌化卡支付](https://openai.com/index/introducing-chatgpt-wallet/) ⭐️ 8.0/10

OpenAI 发布 ChatGPT Wallet，允许符合条件的 ChatGPT Pro 用户通过助手使用 Visa、Mastercard 和美国运通的令牌化卡片付款，智能体无需接触用户的真实卡号。该功能今日起在美国向 18 岁以上、使用美国发行卡的 Pro 订阅用户开放。每笔购买都要求用户核对商品与金额，并通过 Face ID 或指纹确认，支付网络下发替代真实卡号的支付令牌。

telegram · zaihuapd · 11月13日 15:43

**「背景：令牌化支付与智能体代付」** ChatGPT Wallet 的支付依赖于卡组织的令牌化机制：由支付网络下发一个替代真实卡号的支付令牌，商户与智能体只接触令牌，因此智能体代付时不需要拿到用户的卡号。据 CNBC 报道，参与合作的美国运通、万事达和 Visa 卡持有人仍保留原有的信用卡返现与积分；OpenAI 同时发布了帮助商家支持顾客用智能体下单的工具与指引。

**「影响」** 对符合条件的用户，结账时需逐笔完成生物识别确认；非美国 Pro 订阅用户或使用非美国发行卡的用户目前无法使用这一支付方式。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://openai.com/index/introducing-chatgpt-wallet/">Introducing ChatGPT Wallet | OpenAI</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/openai-chatgpt-wallet-dot-purchases.html">OpenAI &#x27;s ChatGPT Wallet allows &#x27;dots&#x27; AI agents to make purchases</a></li>

</ul>
</details>

**标签**: `#OpenAI`, `#ChatGPT`, `#payments`, `#agentic commerce`, `#security`

---

<a id="item-tech-news-3"></a>
### [Python 早期贡献者 Tim Peters 去世，享年 74 岁](https://x.com/Itsfoss/status/2120957452937998716) ⭐️ 7.0/10

Python 创造者 Guido van Rossum 宣布，Python 早期贡献者 Tim Peters 去世，享年 74 岁。Peters 是 Python 的第二位真实用户，也是 Timsort 排序算法的作者，并撰写了《Python 之禅》（PEP 20）。他还在 Python 软件基金会董事会任职 13 年。

telegram · zaihuapd · 11月13日 09:55

**「背景」** PEP 20《Python 之禅》最初是 Tim Peters 于 1999 年在 Python 邮件列表中发布的一组设计原则，并非一开始就是正式规范；其中 19 条成文，第 20 条特意留空，交由 Guido van Rossum 填写。这组原则后来成为 Python 社区常被引用的编程哲学，也是 Peters 在语言文化层面最具辨识度的贡献之一。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Zen_of_Python">Zen of Python - Wikipedia</a></li>

</ul>
</details>

**标签**: `#Python`, `#open source`, `#Timsort`, `#PEP 20`, `#community`

---

<a id="item-tech-news-4"></a>
### [微软 Outlook、Teams 与 Copilot 全球中断逾 12 小时](https://www.reuters.com/technology/microsoft-365-outlook-down-thousands-us-users-downdetector-shows-2026-11-12/) ⭐️ 7.0/10

微软 Outlook、Teams 和 Copilot 在 11 月 13 日发生全球性中断，持续超过 12 小时；微软将原因归为服务器问题，称未发现恶意活动，并表示已扩大修复范围、看到回稳迹象，但相关服务当时仍处于故障状态。澳大利亚、日本和美国部分政府机构受到影响，Euronext 的邮件受阻，台湾有金融机构改用传真确认交易。报道指出，这是微软 365 服务今年第二次中断。

telegram · zaihuapd · 11月13日 12:21

**「背景」** Outlook、Teams 和 Copilot 都属于微软 365 的云端服务，用户端功能依赖微软服务器端的可用性，因此服务器故障会同时波及多个应用和地区。来源还称，这是微软 365 服务今年第二次中断。

**「影响」** 依赖 Microsoft 365 的机构在邮件和 Teams 不可用时需要启用备用通信渠道；台湾金融机构改用传真确认交易，说明关键交易确认流程仍需保留离线备份方案。

**标签**: `#Microsoft 365`, `#Outlook`, `#Teams`, `#service outage`, `#cloud reliability`

---

<a id="item-tech-news-5"></a>
### [DeepSeek 开放应用 API，集成搜索、文件与语音能力](https://mp.weixin.qq.com/s/78KBHc4-4N5b2vfL9SkutQ) ⭐️ 7.0/10

DeepSeek 开放了一套应用 API：开发者在原有 API 中开启相应参数，即可让对话获得深度思考搜索、文件输入、链接阅读和语音能力，工具调用与上下文拼接由服务端自动完成。Search、Fetch、OCR、ASR、TTS 也可单独调用，V4.1-Flash 模型已在三个接口支持。官方同时开源了可导入历史对话的前端 Demo，支持将 DeepSeek 网页端本地部署。上述信息来自一篇微信推文，未披露具体接口名称、计费方式或调用配额。

telegram · zaihuapd · 11月13日 14:27

**「背景」** 服务端工具调用指的是：开发者在请求中开启相应参数后，由 API 服务端完成搜索、读取链接或文件、语音识别与合成等工具的调用以及上下文拼接，开发者不必在客户端逐项编排。DeepSeek 的 API 文档称，V4.1-Flash（deepseek-flash）已在 Messages、Responses 和 Chat Completions 三个接口中支持这些能力，Search、Fetch、OCR、ASR、TTS 也可作为独立 API 单独调用。

**「影响」** 对已接入 DeepSeek API 的开发者，可以直接在聊天流程中组合搜索、文件或链接解析和语音能力，减少自行拼接 OCR、ASR、TTS 与工具调用链的工作量；但现有公开信息未说明这些能力的计费和限额，且模型支持范围有限，接入前应核对官方文档并按 V4.1-Flash 的可用接口做兼容性测试。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://api-docs.deepseek.com/news/news261113/">The full DeepSeek App experience, now via API | DeepSeek API Docs</a></li>

</ul>
</details>

**标签**: `#DeepSeek`, `#API`, `#AI agents`, `#multimodal`, `#open source`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [CNBC：卢特尼克之子执掌的坎托减持英伟达，引发利益冲突质疑](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

CNBC 报道，由美国商务部长霍华德·卢特尼克的两个儿子布兰登和凯尔执掌的坎托·菲茨杰拉德公司，在 2025 年 9 月至 2026 年 3 月间，将其向监管机构申报的英伟达持股数量削减约 49%，从约 350 万股降至 178 万股，申报市值从 6.52 亿美元降至 3.10 亿美元；同一时期，该公司仍参与为英伟达合作伙伴安排数十亿美元融资的业务。此前 Axios 报道称，卢特尼克多次抵触对涉嫌向中国转运英伟达芯片的新加坡公司 Megaspeed 采取行动。英伟达 CEO 黄仁勋已于周四辞职；坎托发言人称，公司在英伟达的自营持仓“无关紧要”，CNBC 也表示，没有证据显示坎托持股变化与相关警告有关，或存在信息不当传递。

rss · CNBC Finance · 11月13日 23:42

**「背景」** 卢特尼克于 2025 年 2 月离开华尔街出任美国商务部长，而商务部正是主管出口管制与实体清单的部门，坎托·菲茨杰拉德此后由其子布兰登和凯尔执掌。英伟达 CEO 黄仁勋已于 11 月 12 日辞职，由首席财务官科莱特·克雷斯暂代 CEO。

**「影响」** 是否将企业列入限制出口的“实体清单”由商务部决定，而财政部长贝森特称，财政部、国防部、国务院和美国贸易代表办公室已支持把 Megaspeed 列入清单数月，这意味着相关对华芯片转运限制的落地时间仍不确定，进而影响英伟达及其依赖出口许可的客户的供应链安排。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Announces-CEO-Transition/">NVIDIA Corporation - NVIDIA Announces CEO Transition</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#Howard Lutnick`, `#Cantor Fitzgerald`, `#export controls`, `#conflicts of interest`

---

<a id="item-finance-news-2"></a>
### [芝加哥联储主席古尔斯比：美联储在通胀上“肯定还有工作要做”](https://www.cnbc.com/2026/11/13/chicago-feds-goolsbee-says-central-bank-has-definitely-got-work-to-do-on-inflation.html) ⭐️ 8.0/10

芝加哥联储主席古尔斯比 11 月 13 日表示，美联储在通胀问题上“肯定还有工作要做”，此前 10 月生产者价格指数（PPI）同比上涨 6.5%，为 2022 年 11 月以来最高。据芝商所 FedWatch，市场完全计入 12 月 8-9 日会议加息 25 个基点（0.25 个百分点）的预期。

rss · CNBC Finance · 11月13日 14:22

**「背景」** 美联储的通胀目标是 2%。古尔斯比称通胀已近六年高于目标、近期没有进展，并把部分需求过热归因于 AI 数据中心建设；他目前不是联邦公开市场委员会（FOMC）投票委员，2027 年才将拥有投票权。

**「影响」** 若美联储在 12 月加息，新申请贷款或持有浮动利率贷款的家庭和企业将面临更高的借贷成本。

**标签**: `#Federal Reserve`, `#inflation`, `#PPI`, `#monetary policy`, `#rate hike expectations`

---