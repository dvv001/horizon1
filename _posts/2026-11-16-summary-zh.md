---
layout: default
title: "Horizon Summary: 2026-11-16 (ZH)"
date: 2026-11-16
lang: zh
---

> 从 36 条内容中筛选出 6 条重要资讯。

---

**科技新闻**
1. [Meta FAIR/NYU：视觉编码器预训练非必需，视觉专属参数不可省](#item-tech-news-1) ⭐️ 8.0/10
2. [美团开源 LongCat-2.5：称全程用华为升腾训练](#item-tech-news-2) ⭐️ 8.0/10
3. [Raschka 解析现代 LLM 的位置嵌入](#item-tech-news-3) ⭐️ 7.0/10
4. [MacBook Pro OLED 屏幕的 PWM 闪烁争议](#item-tech-news-4) ⭐️ 7.0/10

**财经新闻**
1. [卢特尼克因英伟达关系与对华芯片执法面临审查](#item-finance-news-1) ⭐️ 7.0/10
2. [美法官驳回美光、三星、SK 海力士撤销 DRAM 价格操纵案动议](#item-finance-news-2) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Meta FAIR/NYU：视觉编码器预训练非必需，视觉专属参数不可省](https://www.reddit.com/r/MachineLearning/comments/1xx1k2o/meta_fair_nyu_unbundling_multimodal_vision/) ⭐️ 8.0/10

Meta FAIR 与 NYU 作者报告了一项大规模消融研究：在相同数据和同等总计算预算下从零训练 200 多个多模态大模型，主比较使用 Qwen3-1.7B 和 4B 骨干、配置 0.4B 视觉参数，规模覆盖 0.6B 到 6.4B，评测包含 Cambrian 的 16 个 448 像素 VQA 基准和 12 个语言基准。作者称，单独进行编码器预训练是可选的：用四种目标预训练的编码器在匹配计算下最多只能与随 LLM 从零训练的编码器打平，将 MetaCLIP 预训练延长 6.5 倍虽把 ImageNet 线性探测准确率从 80.4% 提到 84.4%，却没有提升 VQA。视觉专属参数则不可省：无编码器模型在各规模都落后，追上约需 3 倍计算；把编码器参数让给 LLM 会改善文本而非 VQA。作者还称编码器置于 LLM 之前并非必需：将零初始化的视觉专属权重加入前 8 层、文本不使用这些权重的“in-fusion”在 1.7B 到 6.4B 与编码器相当，首 token 时间低约 13%，1.7B 下 VQA 为 45.0，对编码器 44.4、共享参数 42.3、最后 8 层 35.1；上述均为论文作者报告，尚未见独立复现。

reddit · r/MachineLearning · /u/trungh98 · 11月15日 17:38

**「背景」** 多模态语言模型通常把视觉编码器当作一个整体：它同时引入上游预训练形成的视觉先验、专用于视觉的模型容量，以及位于语言模型之前的融合位置。该论文指出，已发布模型在数据、架构和算力上各不相同，因此仅靠横向比较无法判断究竟是哪一项设计选择影响了下游 VQA 表现。

**「对开发者的影响」** 对构建多模态模型的团队而言，这项消融提示可把预算从独立视觉预训练转向同预算的多模态联合训练，并在 1.7B 至 6.4B 规模评估前 8 层视觉专属分支以降低首 token 延迟；但若选择无编码器路线，需预留约 3 倍计算，且结论来自作者的单一训练配方和 448 像素 VQA/语言评测，迁移到其他数据或高分辨率任务前应自行复现。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/abs/2611.17334">[2611.17334] Unbundling Multimodal Vision Encoding - arXiv.org</a></li>
<li><a href="https://huggingface.co/papers/2611.17334">Paper page - Unbundling Multimodal Vision Encoding</a></li>

</ul>
</details>

**标签**: `#multimodal LLMs`, `#vision encoders`, `#model architecture`, `#pretraining`, `#empirical study`

---

<a id="item-tech-news-2"></a>
### [美团开源 LongCat-2.5：称全程用华为升腾训练](https://the-decoder.com/meituan-releases-a-1-6-trillion-parameter-agent-model-that-never-touched-an-nvidia-gpu/) ⭐️ 8.0/10

美团 LongCat 团队在模型发布一周后公开了 LongCat-2.5 的权重，采用 MIT 许可证、可商用，面向需要自主完成长流程多步骤任务（尤其是编程）的智能体场景。官方称这个约 1.6 万亿参数、每 token 激活约 480 亿参数的模型支持文本、图像和视频输入，训练全程使用华为升腾加速卡、未使用英伟达 GPU。团队报告其在 Terminal Bench v2.1 得分 88.4，略低于 Claude Opus 5 的 89.1；上述硬件与基准成绩均为官方说法，尚缺独立验证。

telegram · zaihuapd · 11月15日 11:08

**「背景」** LongCat-2.5 由美团 LongCat 团队研发，模型本体一周前已发布，此次是补开权重。所谓“智能体模型”指能在较少人工干预下连续执行多步骤任务，Terminal Bench v2.1 则是衡量模型在终端环境下完成这类任务能力的基准，官方给出的 88.4 分即来自该测试。训练硬件成为焦点，是因为高端英伟达 GPU 长期是大模型训练的主流选择，而升腾属于替代路线。

**「采用影响」** MIT 许可证允许商用和修改，团队可自行托管 LongCat-2.5，并将其接入自有的智能体编程流程，无需依赖美团提供的 API。不过，Terminal Bench v2.1 的 88.4 分目前仍是美团单方公布、未经第三方验证，实际选型前应在自己的代码库上复测。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://tpsreport.news/models/longcat-2-5">LongCat - 2 . 5 specs, benchmarks and changelog | TPS</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#agentic coding`, `#Huawei Ascend`, `#LLM training hardware`, `#Terminal Bench`

---

<a id="item-tech-news-3"></a>
### [Raschka 解析现代 LLM 的位置嵌入](https://magazine.sebastianraschka.com/p/understanding-positional-embeddings) ⭐️ 7.0/10

Sebastian Raschka 的杂志于 2026 年 11 月 15 日刊登了一篇技术文章，解释现代大语言模型中的位置嵌入，面向希望理解 Transformer 如何表示序列位置的读者。该文在 Hacker News 上引发讨论，评论把焦点从实现细节扩展到位置嵌入的理论基础。提供的源内容为空，因此文章的具体论点、覆盖范围和示例无法核实；可确认的信息仅来自标题、摘要与评论。

hackernews · vismit2000 · 11月15日 12:14 · [社区讨论](https://news.ycombinator.com/item?id=50506376)

**「背景」** 自注意力本身对 token 顺序是置换等变的：若不额外注入位置信息，模型无法区分同一组 token 的不同排列，因此位置编码是 Transformer 架构中不可缺少的组件。早期模型多采用正弦式绝对位置编码，而按现有技术资料的梳理，现代 LLM 已基本转向 RoPE 等替代方案，这也正是该文所要解释的机制演变脉络。

**「社区讨论」** 评论者 programjames 认为，文章仅涉及位置嵌入的实现理解，真正理解还需要群表示论：位置嵌入是群表示，这一框架可用于推导它们，并把它们参数化为可微分、可学习的对象。该评论以旋转位置编码作为平移群表示的例子，但所给片段在“n 维平移群是阿贝尔群，因此其不可约……”处截断，后续论证无法确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.youtube.com/watch?v=GQPOtyITy54">RoPE ( Rotary positional embeddings ) explained: The... - YouTube</a></li>
<li><a href="https://www.linkedin.com/pulse/understanding-qwen3-deep-dive-architecture-math-nour-gaboussa-a2v6f">Understanding Qwen3: A Deep Dive into the Architecture and Math</a></li>

</ul>
</details>

**标签**: `#positional embeddings`, `#large language models`, `#transformer architecture`, `#rotary embeddings`, `#machine learning theory`

---

<a id="item-tech-news-4"></a>
### [MacBook Pro OLED 屏幕的 PWM 闪烁争议](https://macanorak.com/the-macbook-pros-oled-pwm-problem-when-a-better-display-becomes-worse-to-use/) ⭐️ 7.0/10

一篇分析文章讨论了 MacBook Pro OLED 屏幕的 PWM 调光闪烁及其对实际使用舒适度的影响，关注点落在对闪烁敏感的用户身上。文章涉及 240Hz 的 PWM 测量说法，但社区评论并未形成一致结论。评论者还围绕闪烁敏感、屏幕参数与个体体验展开了争论。

hackernews · MacAnorak · 11月15日 13:15 · [社区讨论](https://news.ycombinator.com/item?id=50506719)

**「背景」** OLED 屏幕常用 PWM（脉冲宽度调制）调光：通过快速开关像素并改变占空比来调节亮度，其开关频率和波形可能让部分用户感到闪烁或不适。传统上以“闪烁融合阈值”描述闪烁光看起来稳定的频率，但《Scientific Reports》的一项研究显示，当显示内容含有高频空间边缘时，人眼可感知超过 500 Hz 的闪烁伪影，这使单纯依据标称 PWM 频率判断是否舒适存在局限。

**「影响」** 对闪烁敏感的用户来说，OLED 带来的画质提升不一定等于更舒适的使用体验；购买前实际体验不同亮度下的屏幕表现，比只看规格更有参考价值。

**「社区讨论」** 评论者 legitronics 质疑 240Hz 的测量结论，认为串联 OLED 的两层可能各以 480Hz、180 度反相调光，在多数可用亮度下形成约 960Hz 的有效频率。其他评论则把讨论扩展到 CRI、LCD 运动模糊和脑震荡后的屏幕敏感体验，并呼吁更多研究来确定 PWM 敏感人群的规模。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Flicker_fusion_threshold">Flicker fusion threshold - Wikipedia</a></li>
<li><a href="https://www.nature.com/articles/srep07861?error=cookies_not_supported&amp;code=6835fca7-06e0-41ad-895e-00e7dbda63ee">Humans perceive flicker artifacts at 500 Hz | Scientific Reports</a></li>

</ul>
</details>

**标签**: `#OLED PWM`, `#display flicker`, `#MacBook Pro`, `#hardware ergonomics`, `#tandem OLED`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [卢特尼克因英伟达关系与对华芯片执法面临审查](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

CNBC 报道，美国商务部长霍华德·卢特尼克正面临审查：他此前执掌、现由其子领导的坎托·菲茨杰拉德与英伟达存在业务关系，而他抵制了对涉嫌经中国走私英伟达芯片的公司的打击；报道并称英伟达 CEO 黄仁勋已于周四辞职。CNBC 根据证券文件分析称，坎托报告的英伟达持股在 2025 年 9 月至 2026 年 3 月间减少 49%，从逾 350 万股降至 178 万股，但报道明确说没有证据表明这一变动与情报警告有关，也没有证据表明卢特尼克向坎托分享了非公开信息。

rss · CNBC Finance · 11月15日 19:58

**「背景」** Megaspeed 是一家被怀疑将英伟达先进人工智能芯片转售至中国的公司，多个机构曾提议将其列入由商务部负责的实体清单（即贸易黑名单），但商务部至今未推进该措施。卢特尼克在 2025 年出任商务部长后，已从康托·菲茨杰拉德（Cantor Fitzgerald）回避，这家公司目前由他的儿子们经营。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.nytimes.com/2026/11/09/business/economy/nvidia-megaspeed-investigation-huang.html">U.S. Commerce Dept . Inquiry Into Megaspeed Was Halted After...</a></li>
<li><a href="https://www.nytimes.com/2026/11/15/us/politics/trump-lutnick-ai-chips-nvidia-cantor-fitzgerald.html">Lutnick Pushed to Weaken Chip Rules That Overlap With His Family...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#U.S. export controls`, `#Commerce Department`, `#conflict of interest`, `#semiconductor industry`

---

<a id="item-finance-news-2"></a>
### [美法官驳回美光、三星、SK 海力士撤销 DRAM 价格操纵案动议](https://www.tomshardware.com/tech-industry/big-tech/judge-denies-motion-to-dismiss-dram-price-fixing-lawsuit-against-micron-samsung-and-sk-hynix-says-chipmakers-acted-like-hawks-flying-in-formation-finds-evidence-of-dram-collusion-plausible-after-500-percent-price-surge) ⭐️ 7.0/10

美国法官 Noël Wise 驳回美光、三星和 SK 海力士撤销 DRAM 价格操纵集体诉讼的动议，裁定原告提出的同步限制供应证据足以让案件继续审理；这仅是程序性裁决，尚未认定三家公司违法。17 名个人和小企业原告指称，三家公司一年内四次平行限制 DRAM 供应，使价格最高上涨 500%，三家公司须在 12 月 7 日前回应。

telegram · zaihuapd · 11月15日 16:39

**「背景」** 这并非美国首次审理 DRAM 价格操纵指控：在更早的一起刑事案件中，三星与海力士（现 SK 海力士）认罪，两家合计缴纳 7.31 亿美元刑事罚款。本次裁定属程序性决定，只是允许诉讼继续，并不等于认定三家厂商违法。

**「影响」** 这一程序性裁定使针对美光、三星和 SK 海力士的集体诉讼继续推进，三家厂商须应诉，提出索赔的 17 名个人和小企业买家也可继续追索；法院尚未认定任何一方负有责任。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.techpowerup.com/243767/samsung-micron-and-hynix-accused-of-dram-price-fixing">Samsung , Micron , and Hynix Accused of DRAM Price Fixing</a></li>
<li><a href="https://litnews.ai/articles/garciaguirre-samsung-sk-hynix-micron-dram-conspiracy-suit-survives-dismissal">Judge Refuses to Dismiss DRAM Supply Conspiracy Suit Against...</a></li>

</ul>
</details>

**标签**: `#DRAM`, `#antitrust`, `#price-fixing litigation`, `#semiconductors`, `#Micron/Samsung/SK Hynix`

---