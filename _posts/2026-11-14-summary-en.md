---
layout: default
title: "Horizon Summary: 2026-11-14 (EN)"
date: 2026-11-14
lang: en
---

> From 39 items, 7 important content pieces were selected

---

**Technology News**
1. [TorchTitan trains 1T-parameter MoE at 1,300 tokens/s per GPU on 384 GH200s](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI Launches ChatGPT Wallet With Tokenized Card Payments](#item-tech-news-2) ⭐️ 8.0/10
3. [Python early contributor Tim Peters dies at 74](#item-tech-news-3) ⭐️ 7.0/10
4. [Microsoft Outlook, Teams and Copilot outage passes 12 hours](#item-tech-news-4) ⭐️ 7.0/10
5. [DeepSeek opens application APIs for search, files, voice and tool calling](#item-tech-news-5) ⭐️ 7.0/10

**Financial News**
1. [Lutnick faces conflict questions over sons&\#x27; firm and Nvidia](#item-finance-news-1) ⭐️ 8.0/10
2. [Goolsbee Says Fed Has More Work to Do on Inflation](#item-finance-news-2) ⭐️ 8.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [TorchTitan trains 1T-parameter MoE at 1,300 tokens/s per GPU on 384 GH200s](https://www.reddit.com/r/MachineLearning/comments/1xvce5h/scaling_to_1t_moe_on_torchtitan_p/) ⭐️ 8.0/10

A team reports training a ~1T-parameter mixture-of-experts model on 384 GH200 GPUs \(the JUPITER machine\) with TorchTitan, reaching about 1,300 tokens/s per GPU — a 14X gain over their starting point, where an 84-second step spent 68 seconds waiting on InfiniBand \(~25 GB/s per GPU versus 6X faster NVLink\). The configuration is 384-way FSDP plus 4-way expert parallelism held strictly inside each node, with pipeline parallelism deliberately skipped to keep iteration fast. Reported wins came from full activation checkpointing \(4X\), offloading checkpoint activations to Grace over the 900 GB/s C2C link, switching to Muon to reach 64k-token sequences, sharding experts whole via FlexShard so Newton-Schulz runs locally, and moving that Newton-Schulz work to the GPU even with host-resident parameters \(optimizer step 42 s to ~2 s, +35%\). Further gains were FP8 expert all-gather with blockwise scales \(+18%\), attention-cost bucketing that cut the worst-rank imbalance from 7.9X to 1.15X of average \(+13%\), and a caching-allocator fix that moved ~21 GiB of collective temporaries off side streams \(zero allocator retries, 13.5 GiB lower peak reserved memory, +21% throughput\). This is a community post summarizing Domyn and PyTorch blog writeups, not a peer-reviewed benchmark, and the authors note that group-limited routing&\#x27;s +7% comes with an unresolved concern that constraining where the router can send tokens may hurt training.

reddit · r/MachineLearning · /u/f14-bertolotti · Nov 13, 16:28

**「What TorchTitan and the GH200 cluster provide」** TorchTitan is the PyTorch project&\#x27;s open-source framework for large-model pretraining, which lets teams combine sharding strategies — FSDP, expert parallelism, and pipeline parallelism — instead of building a distributed-training stack themselves. The hardware context is JUPITER, Europe&\#x27;s shared public exascale system, whose GH200 nodes pair a Hopper GPU with a Grace CPU over a 900 GB/s C2C link while inter-node traffic runs over roughly 25 GB/s per GPU of InfiniBand, a bandwidth hierarchy that constrains every sharding decision. External coverage of the underlying PyTorch and Domyn write-ups attributes the work to the EUROPA consortium and describes a 951.9B-parameter MoE trained on 384 GH200 GPUs per replica, scaling to 1,536 GPUs across four replicas.

**「Impact」** The transferable pieces for other TorchTitan users are specific: the GPU-side Newton-Schulz path the authors contributed upstream, and FSDP2&\#x27;s private \`unshard\_async\_op\` flag, which they say is on its way to becoming a public API, so teams hitting allocator retries at high HBM utilization can move collective temporaries onto the compute stream without forking. The headline 14X is measured against their own baseline step rather than against other frameworks, and the design depends on expert parallelism fitting within a single node&\#x27;s NVLink domain, a constraint that would need revisiting wherever the expert-parallel degree exceeds the size of a fast interconnect island.

<details><summary>References</summary>
<ul>
<li><a href="https://pytorch.org/blog/training-a-1t-parameter-moe-on-eu-public-infrastructure-with-pytorch-and-torchtitan/">Training a 1T-Parameter MoE on EU public ... - PyTorch</a></li>
<li><a href="https://daily.dev/posts/training-a-1t-parameter-moe-on-eu-public-infrastructure-with-pytorch-and-torchtitan-tjfwzdwty">Training a 1T-Parameter MoE on EU public infrastructure...</a></li>

</ul>
</details>

**Tags**: `#MoE`, `#distributed training`, `#TorchTitan`, `#PyTorch`, `#GH200`

---

<a id="item-tech-news-2"></a>
### [OpenAI Launches ChatGPT Wallet With Tokenized Card Payments](https://openai.com/index/introducing-chatgpt-wallet/) ⭐️ 8.0/10

OpenAI launched ChatGPT Wallet, letting ChatGPT Pro subscribers in the US who are 18 or older pay through the assistant using US-issued Visa, Mastercard, or American Express cards. The wallet uses payment-network tokens instead of exposing the user&\#x27;s real card number, and each purchase requires the user to review the item and amount and confirm with Face ID or a fingerprint. OpenAI said the feature is available starting today.

telegram · zaihuapd · Nov 13, 15:43

**「Background」** ChatGPT Wallet relies on card-network tokenization: instead of exposing a real card number to the agent or merchant, the payment network issues a substitute token tied to the purchase. OpenAI is distributing the wallet through its dots agent product, and CNBC reports that participating cardholders keep their existing card rewards.

**「Impact」** For eligible users, the practical change is that an assistant can initiate a purchase while the card number stays hidden behind a token, but checkout still requires per-transaction review and biometric approval. That keeps the feature limited to supervised purchases and makes a US Pro subscription and a US-issued card prerequisites.

<details><summary>References</summary>
<ul>
<li><a href="https://openai.com/index/introducing-chatgpt-wallet/">Introducing ChatGPT Wallet | OpenAI</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/openai-chatgpt-wallet-dot-purchases.html">OpenAI &#x27;s ChatGPT Wallet allows &#x27;dots&#x27; AI agents to make purchases</a></li>

</ul>
</details>

**Tags**: `#OpenAI`, `#ChatGPT`, `#payments`, `#agentic commerce`, `#security`

---

<a id="item-tech-news-3"></a>
### [Python early contributor Tim Peters dies at 74](https://x.com/Itsfoss/status/2120957452937998716) ⭐️ 7.0/10

Guido van Rossum has reportedly announced the death of Tim Peters, an early contributor to Python, at age 74, according to a Telegram post citing It&\#x27;s FOSS. The item credits Peters as Python&\#x27;s second real user, the author of the Timsort sorting algorithm, the writer of PEP 20 \(&quot;The Zen of Python&quot;\), and a 13-year member of the Python Software Foundation board. The source gives no cause or date of death, so the announcement itself rests on the reported statement rather than an independently verified record.

telegram · zaihuapd · Nov 13, 09:55

**「Background」** Peters wrote the 19 aphorisms that became PEP 20, “The Zen of Python,” posting them to the Python mailing list in 1999 and leaving a 20th principle for Guido van Rossum to fill in. A Python discussion forum post by van Rossum dated November 11, 2026, said Peters had died on July 15 of that year.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Zen_of_Python">Zen of Python - Wikipedia</a></li>
<li><a href="https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028">In Memoriam: Tim Peters 1952–2026 - Core Development...</a></li>

</ul>
</details>

**Tags**: `#Python`, `#open source`, `#Timsort`, `#PEP 20`, `#community`

---

<a id="item-tech-news-4"></a>
### [Microsoft Outlook, Teams and Copilot outage passes 12 hours](https://www.reuters.com/technology/microsoft-365-outlook-down-thousands-us-users-downdetector-shows-2026-11-12/) ⭐️ 7.0/10

Microsoft Outlook, Teams and Copilot remained down on November 13, with the disruption lasting more than 12 hours and affecting enterprise and government communications worldwide. Microsoft attributed the outage to a server problem, said it had found no malicious activity, and reported that it had expanded remediation and was seeing signs of stabilization. Australian, Japanese and some US government agencies were affected, Euronext email was disrupted, and financial institutions in Taiwan switched to fax to confirm trades. The incident was Microsoft 365&\#x27;s second service disruption this year.

telegram · zaihuapd · Nov 13, 12:21

**「Why one fault hit multiple services」** Microsoft 365 is an integrated cloud suite, so Outlook, Teams and Copilot rely on shared Microsoft-operated backend services rather than separate on-premises systems; a server-side fault can therefore disrupt mail, chat and assistant features across regions at once. The report describes this as Microsoft 365&\#x27;s second service interruption this year, following an earlier disruption in 2026.

**「Impact」** Affected government agencies and financial-market participants lost normal email and chat channels, forcing at least some trading operations in Taiwan onto fax confirmations while Euronext email was disrupted.

**Tags**: `#Microsoft 365`, `#Outlook`, `#Teams`, `#service outage`, `#cloud reliability`

---

<a id="item-tech-news-5"></a>
### [DeepSeek opens application APIs for search, files, voice and tool calling](https://mp.weixin.qq.com/s/78KBHc4-4N5b2vfL9SkutQ) ⭐️ 7.0/10

DeepSeek has opened a suite of application APIs that let developers enable deep-thinking search, file input, link reading and voice in chat applications by setting parameters in the existing API, with the server handling tool calls and context assembly. The V4.1-Flash model is supported across three interfaces, while Search, Fetch, OCR, ASR and TTS can also be called separately. DeepSeek also open-sourced a frontend chat demo that can import conversation history; the source is a secondary Telegram post and provides no benchmarks or primary API documentation.

telegram · zaihuapd · Nov 13, 14:27

**「Background」** DeepSeek&\#x27;s documentation lists V4.1-Flash \(deepseek-flash\) as supporting the new capabilities across three API surfaces—Messages, Responses, and Chat Completions—so developers enable them through parameters on existing endpoints. The model is a 763B-parameter image-text-to-text system, and Search, Fetch, OCR, ASR, and TTS are additionally available as standalone APIs.

**「Impact」** Developers building chat applications can add these capabilities through existing API parameters rather than assembling separate search, OCR, speech and tool-calling pipelines themselves. The post names only V4.1-Flash for the three built-in interfaces, so teams using other models should verify support before relying on the bundled behavior.

<details><summary>References</summary>
<ul>
<li><a href="https://api-docs.deepseek.com/news/news261113/">The full DeepSeek App experience, now via API | DeepSeek API Docs</a></li>
<li><a href="https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash">deepseek -ai/ DeepSeek - V 4 . 1 - Flash · Hugging Face</a></li>

</ul>
</details>

**Tags**: `#DeepSeek`, `#API`, `#AI agents`, `#multimodal`, `#open source`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Lutnick faces conflict questions over sons&\#x27; firm and Nvidia](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

Commerce Secretary Howard Lutnick is facing conflict-of-interest questions after CNBC reported that Cantor Fitzgerald, now run by his sons, cut its reported Nvidia share count by 49% between September 2025 and March 2026, from about 3.5 million to 1.78 million shares, while maintaining business ties to the chipmaker. The report links the scrutiny to a China chip-smuggling probe and Nvidia CEO Jensen Huang&\#x27;s resignation, but says there is no evidence the holdings changes were tied to intelligence warnings or that Lutnick shared nonpublic information.

rss · CNBC Finance · Nov 13, 23:42

**「Background」** The scrutiny follows Nvidia CEO Jensen Huang&\#x27;s resignation effective Nov. 12, 2026, after reports of extramarital affairs, including with an alleged Chinese spy. The Commerce Department that Lutnick heads administers the entity list, the restricted-party roster used to block foreign firms from buying U.S. technology — the lever at issue in the Megaspeed chip-smuggling probe.

<details><summary>References</summary>
<ul>
<li><a href="https://wccftech.com/nvidia-intervened-federal-investigation-megaspeed-ai-chip-smuggling-probe/">NVIDIA Allegedly Became A Roadblock For Federal Investigation ...</a></li>
<li><a href="https://www.theguardian.com/technology/2026/nov/12/nvidia-ceo-jensen-huang-resigns">Jensen Huang resigns as Nvidia CEO after alleged affairs</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#Howard Lutnick`, `#Cantor Fitzgerald`, `#export controls`, `#conflicts of interest`

---

<a id="item-finance-news-2"></a>
### [Goolsbee Says Fed Has More Work to Do on Inflation](https://www.cnbc.com/2026/11/13/chicago-feds-goolsbee-says-central-bank-has-definitely-got-work-to-do-on-inflation.html) ⭐️ 8.0/10

Chicago Fed President Austan Goolsbee said the Federal Reserve &quot;has definitely got work to do&quot; to restore credibility on inflation, after October producer prices rose 6.5% from a year earlier, the highest since November 2022. Markets are fully pricing a quarter-point interest-rate increase at the Dec. 8-9 FOMC meeting, according to CME Group&\#x27;s FedWatch.

rss · CNBC Finance · Nov 13, 14:22

**「Background」** The Fed targets 2% inflation; Goolsbee said inflation has been above that for almost six years and recently has not been improving, with the AI data-center buildout adding demand pressure. Goolsbee is not currently an FOMC voter but will be in 2027.

**Tags**: `#Federal Reserve`, `#inflation`, `#PPI`, `#monetary policy`, `#rate hike expectations`

---