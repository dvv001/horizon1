---
layout: default
title: "Horizon Summary: 2026-11-16 (EN)"
date: 2026-11-16
lang: en
---

> From 36 items, 6 important content pieces were selected

---

**Technology News**
1. [Meta FAIR/NYU ablation: vision needs its own parameters, not encoder pretraining](#item-tech-news-1) ⭐️ 8.0/10
2. [Meituan releases LongCat-2.5, claiming all-Huawei-Ascend training](#item-tech-news-2) ⭐️ 8.0/10
3. [Technical Explainer on Positional Embeddings in Modern LLMs](#item-tech-news-3) ⭐️ 7.0/10
4. [MacBook Pro OLED PWM flicker analysis draws dispute over measured frequency](#item-tech-news-4) ⭐️ 7.0/10

**Financial News**
1. [Lutnick faces scrutiny over Nvidia ties and China chip crackdown](#item-finance-news-1) ⭐️ 7.0/10
2. [Judge Allows DRAM Price-Fixing Case Against Micron, Samsung and SK Hynix to Proceed](#item-finance-news-2) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Meta FAIR/NYU ablation: vision needs its own parameters, not encoder pretraining](https://www.reddit.com/r/MachineLearning/comments/1xx1k2o/meta_fair_nyu_unbundling_multimodal_vision/) ⭐️ 8.0/10

Meta FAIR and NYU researchers ran a controlled ablation of multimodal vision encoder design choices across 200+ models, all trained from scratch \(LLM included\) on the same data, with encoder pretraining charged against the same compute budget as multimodal training. Main comparisons used Qwen3-1.7B and 4B backbones with 0.4B parameters of vision capacity, plus a scaling ladder from 0.6B to 6.4B, evaluated on 16 Cambrian VQA benchmarks at 448 px and 12 language benchmarks. They report that separate encoder pretraining is optional — four pretrained encoders \(contrastive, self-supervised, two captioning objectives\) at best tied a from-scratch encoder at matched compute, and even free pretraining did not help VQA, though pretraining MetaCLIP 6.5x longer raised ImageNet linear-probe accuracy from 80.4% to 84.4%. Vision-only parameters, by contrast, were required: encoder-free models trailed at every size and needed about 3x the compute to catch up, while placement before the LLM proved optional — an &quot;in-fusion&quot; variant adding zero-initialized vision-only weights to the LLM&\#x27;s first 8 layers matched the encoder from 1.7B to 6.4B with about 13% lower time to first token \(45.0 VQA at 1.7B versus 44.4 for the encoder, 42.3 when text shares the weights, and 35.1 when the branches sit in the last 8 layers\). The results are reported by an author of the work via a preprint on alphaXiv and a project blog, not an independently verified or peer-reviewed measurement.

reddit · r/MachineLearning · /u/trungh98 · Nov 15, 17:38

**「Why the encoder question is unsettled」** Most multimodal LLMs pair the language model with a vision encoder pretrained separately, but recent published recipes have diverged — some train the encoder jointly from scratch and others remove it — so the field has no agreed default. The paper&\#x27;s premise is that a &quot;standard&quot; encoder silently bundles three distinct decisions: an upstream visual prior from pretraining, parameters reserved for vision tokens, and pre-fusion placement before the multimodal backbone. Because released models differ in data, architecture, and compute, comparing them cannot isolate the effect of any single choice, which is what motivates a controlled ablation that separates the three.

**「For model builders」** For teams assembling MLLMs at roughly 1B-6B backbone scale, the reported result suggests spending compute on dedicated vision-only parameters rather than on a separately pretrained encoder, since dropped pretraining at best tied from-scratch training in this setup. Going encoder-free is the costlier option in these experiments: models without vision-only parameters needed about 3x the compute to match, and reallocating the encoder&\#x27;s parameters to the LLM improved text scores but not VQA. The in-fusion variant is the one architecture change with a reported serving benefit — parity with a standard encoder plus about 13% lower time to first token — though all figures come from one compute-matched regime with Qwen3 backbones, 0.4B vision capacity, and 448 px Cambrian VQA benchmarks.

<details><summary>References</summary>
<ul>
<li><a href="https://arxiv.org/abs/2611.17334">[2611.17334] Unbundling Multimodal Vision Encoding - arXiv.org</a></li>
<li><a href="https://huggingface.co/papers/2611.17334">Paper page - Unbundling Multimodal Vision Encoding</a></li>

</ul>
</details>

**Tags**: `#multimodal LLMs`, `#vision encoders`, `#model architecture`, `#pretraining`, `#empirical study`

---

<a id="item-tech-news-2"></a>
### [Meituan releases LongCat-2.5, claiming all-Huawei-Ascend training](https://the-decoder.com/meituan-releases-a-1-6-trillion-parameter-agent-model-that-never-touched-an-nvidia-gpu/) ⭐️ 8.0/10

Meituan&\#x27;s LongCat team published the weights for LongCat-2.5 one week after the model&\#x27;s official launch, under an MIT license that permits commercial use. The model is designed for autonomous long-horizon, multi-step tasks, especially coding, and activates about 48 billion parameters per token while accepting text, image, and video inputs. Meituan says the model was trained entirely on Huawei Ascend accelerators rather than Nvidia GPUs, and reports a Terminal Bench v2.1 score of 88.4, slightly below Claude Opus 5&\#x27;s 89.1. The training-hardware and benchmark claims have not been independently confirmed.

telegram · zaihuapd · Nov 15, 11:08

**「Context」** An open-weight release means the trained parameters are published for others to download and reuse, rather than the model being available only through an API. Meituan released LongCat-2.5&\#x27;s weights under the MIT license, which permits commercial use, and designed the model for agents that carry out long, multi-step tasks, especially coding work.

**「What it means for adopters」** Because the weights are MIT-licensed and the model activates roughly 48B of its 1.6T parameters per token, teams can self-host, commercially deploy, and fine-tune LongCat-2.5 without per-token licensing constraints, and one report says it was offered free inside OpenCode for a two-week window as a low-cost way to trial it on repository-level coding work. The 88.4 Terminal Bench v2.1 score — up from a claimed 70.8 for LongCat-2.0 — is Meituan&\#x27;s own figure and unverified by third parties, so adoption decisions should rest on internal evaluation rather than the published benchmark.

<details><summary>References</summary>
<ul>
<li><a href="https://lmspeed.net/model/longcat-2-5">LongCat - 2 . 5 API Pricing &amp; Benchmarks | LMSpeed</a></li>
<li><a href="https://www.youtube.com/watch?v=xYo_lFvVKpY">LongCat 2 . 5 Is Now FREE on OpenCode?! - YouTube</a></li>
<li><a href="https://tpsreport.news/models/longcat-2-5">LongCat - 2 . 5 specs, benchmarks and changelog | TPS</a></li>

</ul>
</details>

**Tags**: `#open-weight models`, `#agentic coding`, `#Huawei Ascend`, `#LLM training hardware`, `#Terminal Bench`

---

<a id="item-tech-news-3"></a>
### [Technical Explainer on Positional Embeddings in Modern LLMs](https://magazine.sebastianraschka.com/p/understanding-positional-embeddings) ⭐️ 7.0/10

A technical explainer published on Sebastian Raschka&\#x27;s newsletter site walks through how positional embeddings are implemented in modern large language models, with rotary positional embeddings among the approaches it covers. The piece is framed as an implementation-level explanation of transformer architecture rather than new research, a release, or a benchmark result. Only the article link and topic metadata were supplied with this item, so the specific claims, code examples, and model comparisons in the text could not be verified here.

hackernews · vismit2000 · Nov 15, 12:14 · [Discussion](https://news.ycombinator.com/item?id=50506376)

**「Background」** Transformer self-attention is natively permutation-equivariant, meaning it has no inherent notion of token order, so positional information must be injected explicitly. Earlier transformer designs relied on fixed sinusoidal embeddings, but modern LLMs have largely moved to alternatives such as rotary positional embeddings \(RoPE\). The article organizes its explanation around which positional-embedding choices appear in 2026 open-weight models.

**「Community Discussion」** Commenter programjames argued that an implementation-focused treatment is not enough, contending that positional embeddings are fundamentally group representations and that this framing is how they are derived and parameterized to be differentiable and learnable; as an example, they described rotary positional embeddings as representations of the translation group, whose abelian structure makes its irreducible representations one-dimensional. The supplied excerpt cuts off mid-argument, so the remainder of that case is not visible.

<details><summary>References</summary>
<ul>
<li><a href="https://magazine.sebastianraschka.com/p/understanding-positional-embeddings">Understanding Positional Embeddings in Modern LLMs</a></li>
<li><a href="https://www.youtube.com/watch?v=GQPOtyITy54">RoPE ( Rotary positional embeddings ) explained: The... - YouTube</a></li>
<li><a href="https://www.linkedin.com/pulse/understanding-qwen3-deep-dive-architecture-math-nour-gaboussa-a2v6f">Understanding Qwen3: A Deep Dive into the Architecture and Math</a></li>

</ul>
</details>

**Tags**: `#positional embeddings`, `#large language models`, `#transformer architecture`, `#rotary embeddings`, `#machine learning theory`

---

<a id="item-tech-news-4"></a>
### [MacBook Pro OLED PWM flicker analysis draws dispute over measured frequency](https://macanorak.com/the-macbook-pros-oled-pwm-problem-when-a-better-display-becomes-worse-to-use/) ⭐️ 7.0/10

MacAnorak published an analysis of pulse-width modulation \(PWM\) flicker in the MacBook Pro&\#x27;s OLED display, arguing that a technically better panel can be worse to use for people who are sensitive to flicker. The post&\#x27;s own measurements were not included in the supplied material, so the specific figures under debate come from the surrounding discussion rather than from the article text. That discussion centers on whether the display&\#x27;s PWM behaves at the 240 Hz figure cited, at 480 Hz in the worst case, or at an effective 960 Hz.

hackernews · MacAnorak · Nov 15, 13:15 · [Discussion](https://news.ycombinator.com/item?id=50506719)

**「Why PWM flicker matters」** PWM dimming controls apparent brightness by switching a display&\#x27;s light on and off rapidly and varying the proportion of on-time. The flicker fusion threshold is the frequency at which flickering light appears steady to the average observer, but a Scientific Reports study found that people can perceive flicker artifacts at rates above 500 Hz when a display contains high-frequency spatial edges. That gap between average fusion thresholds and reported sensitivity is central to disputes over whether a laptop&\#x27;s PWM rate is high enough to avoid discomfort.

**「Impact」** For a flicker-sensitive buyer, the number that decides whether the machine is usable is not settled here: commenters argue the effective rate depends on brightness and on how the scope trace is interpreted, so a single quoted PWM frequency may not describe the panel under normal viewing conditions.

**「Community discussion」** Commenter legitronics disputes the 240 Hz figure, proposing that the tandem OLED&\#x27;s two layers each pulse at 480 Hz 180 degrees out of phase, producing an effective 960 Hz across most of the usable brightness range, while achr2 cites a Nature paper reporting that humans can perceive flicker well above twice a display&\#x27;s rate and questions Apple&\#x27;s choice of a low PWM frequency. Others broaden the thread: Velocifyer lists LED color rendering and LCD motion blur as related sensitivities, explosion-s describes screen discomfort following a concussion, and Telaneo asks for research into how many people are actually affected.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Flicker_fusion_threshold">Flicker fusion threshold - Wikipedia</a></li>
<li><a href="https://www.nature.com/articles/srep07861?error=cookies_not_supported&amp;code=6835fca7-06e0-41ad-895e-00e7dbda63ee">Humans perceive flicker artifacts at 500 Hz | Scientific Reports</a></li>

</ul>
</details>

**Tags**: `#OLED PWM`, `#display flicker`, `#MacBook Pro`, `#hardware ergonomics`, `#tandem OLED`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Lutnick faces scrutiny over Nvidia ties and China chip crackdown](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

Commerce Secretary Howard Lutnick is facing scrutiny after Axios reported he resisted a crackdown on suspected Nvidia chip smuggling to China, while Cantor Fitzgerald—the firm his sons now lead—cut its reported Nvidia share count by 49% between September 2025 and March 2026. Nvidia CEO Jensen Huang resigned Thursday amid scrutiny of his ties to a suspected Chinese spy; CNBC reported no evidence that the stake change was tied to intelligence warnings or that Lutnick shared nonpublic information.

rss · CNBC Finance · Nov 15, 19:58

**「Background」** Howard Lutnick spent decades running Cantor Fitzgerald before becoming commerce secretary in 2025, when he recused himself from the firm, which is now led by his sons Brandon and Kyle. His department oversees the entity list — the trade blacklist other agencies wanted used against Megaspeed, a step Commerce has not taken.

<details><summary>References</summary>
<ul>
<li><a href="https://www.nytimes.com/2026/11/09/business/economy/nvidia-megaspeed-investigation-huang.html">U.S. Commerce Dept . Inquiry Into Megaspeed Was Halted After...</a></li>
<li><a href="https://en.wikipedia.org/wiki/Howard_Lutnick">Howard Lutnick - Wikipedia</a></li>
<li><a href="https://www.nytimes.com/2026/11/15/us/politics/trump-lutnick-ai-chips-nvidia-cantor-fitzgerald.html">Lutnick Pushed to Weaken Chip Rules That Overlap With His Family...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#U.S. export controls`, `#Commerce Department`, `#conflict of interest`, `#semiconductor industry`

---

<a id="item-finance-news-2"></a>
### [Judge Allows DRAM Price-Fixing Case Against Micron, Samsung and SK Hynix to Proceed](https://www.tomshardware.com/tech-industry/big-tech/judge-denies-motion-to-dismiss-dram-price-fixing-lawsuit-against-micron-samsung-and-sk-hynix-says-chipmakers-acted-like-hawks-flying-in-formation-finds-evidence-of-dram-collusion-plausible-after-500-percent-price-surge) ⭐️ 7.0/10

A U.S. federal judge denied Micron, Samsung and SK Hynix’s motion to dismiss a DRAM price-fixing class action, ruling that the plaintiffs’ allegations—including four parallel supply restrictions in a year and alleged price increases of up to 500%—are plausible enough to proceed. The ruling is procedural, not a finding of liability; the companies must respond by Dec. 7, with a case-management conference set for January 2027.

telegram · zaihuapd · Nov 15, 16:39

**「Background」** The DRAM industry has faced U.S. price-fixing cases before: Samsung and Hynix previously pleaded guilty and paid a combined $731 million in criminal fines, according to TechPowerUp.

**「What it means」** The ruling keeps the buyers&\#x27; damages claims alive, so the individuals and small businesses alleging overcharges can pursue the three memory makers in court instead of having the case thrown out.

<details><summary>References</summary>
<ul>
<li><a href="https://www.techpowerup.com/243767/samsung-micron-and-hynix-accused-of-dram-price-fixing">Samsung , Micron , and Hynix Accused of DRAM Price Fixing</a></li>
<li><a href="https://litnews.ai/articles/garciaguirre-samsung-sk-hynix-micron-dram-conspiracy-suit-survives-dismissal">Judge Refuses to Dismiss DRAM Supply Conspiracy Suit Against...</a></li>

</ul>
</details>

**Tags**: `#DRAM`, `#antitrust`, `#price-fixing litigation`, `#semiconductors`, `#Micron/Samsung/SK Hynix`

---