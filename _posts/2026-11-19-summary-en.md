---
layout: default
title: "Horizon Summary: 2026-11-19 (EN)"
date: 2026-11-19
lang: en
---

> From 44 items, 13 important content pieces were selected

---

**Technology News**
1. [Google releases Gemini 4 Neon with 1M-token context and $3/$15 pricing](#item-tech-news-1) ⭐️ 8.0/10
2. [Nginx HTTP/2 flaws enable unauthenticated worker code execution; fixes released](#item-tech-news-2) ⭐️ 8.0/10
3. [Microsoft Announces Seven AI Models at Ignite 2026](#item-tech-news-3) ⭐️ 7.0/10
4. [Google DeepMind&\#x27;s Genie 4 is available, but access terms remain unclear](#item-tech-news-4) ⭐️ 7.0/10
5. [Quad9&\#x27;s France exit and the case against DNS piracy blocking](#item-tech-news-5) ⭐️ 7.0/10
6. [From 4004 to 486: A Detailed x86 History](#item-tech-news-6) ⭐️ 7.0/10
7. [Show HN: Interactive Voyager 1 tour reaches a single memory chip](#item-tech-news-7) ⭐️ 7.0/10

**Financial News**
1. [Fed Minutes Signal More Rate Hikes, Flag AI Inflation Risks](#item-finance-news-1) ⭐️ 8.0/10
2. [Tencent Q3: AI spending surges, capital expenditure well above forecasts](#item-finance-news-2) ⭐️ 8.0/10
3. [Fed’s Waller calls for half-point rate hike in December](#item-finance-news-3) ⭐️ 7.0/10
4. [Trump Arrives in Shenzhen for APEC Leaders&\#x27; Meeting](#item-finance-news-4) ⭐️ 7.0/10
5. [China and South Korea announce substantive end to services, investment FTA talks](#item-finance-news-5) ⭐️ 7.0/10
6. [China Proposes Scrapping New-Energy Vehicles With Their Batteries](#item-finance-news-6) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Google releases Gemini 4 Neon with 1M-token context and $3/$15 pricing](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/) ⭐️ 8.0/10

Google released Gemini 4 Neon, a model it says is aimed at fast end-to-end work in complex software engineering, knowledge work, and scientific research, and made it available to developers, enterprises, and Google AI Pro/Ultra subscribers. The supplied announcement lists a 1 million-token context window and pricing of $3 per million input tokens \($0.15 cached\) and $15 per million output tokens. It also claims first place on Artificial Analysis&\#x27;s coding-agent index at 58.6, third overall on its xhigh intelligence index at 61, 65.2% on Terminal-Bench 4.1, and a 32% lower per-task cost than Carbon at the default high setting; these benchmark and cost figures have not been independently verified in the supplied material.

hackernews · yigitdemirag · Nov 18, 21:34 · [Discussion](https://news.ycombinator.com/item?id=50552424)

**「Context」** Google already fields several separately named Gemini models, so Gemini 4 Neon has to be understood relative to its siblings rather than as a single flagship. The source positions Neon partly on cost, saying a default high-tier task is 32% cheaper than on Carbon, while Hacker News commenters describe Carbon as the long-horizon model and Neon as scoring higher overall but lower on research-scale reasoning evaluations such as CritPt. Those comments also reflect confusion over mapping Google&\#x27;s proliferating model names to specific use cases.

**「Cost and compatibility tradeoffs for agent builders」** Teams running coding agents have a concrete comparison to test: at its default high setting, Neon costs 32% less per task than Carbon while scoring 65.2% on Terminal-Bench 4.1 and 58.6 \(\#1\) on the Artificial Analysis Coding Agent Index, so a swap is worth trialing on existing agent workloads. Budgeting from sticker price alone may mislead, however — Artificial Analysis reports Neon \(xhigh\) generating 283M tokens during its evaluation against a 65.1M median, so per-task spend at $3 per million input tokens \($0.15 cached\) and $15 per million output tokens depends heavily on how verbose the model is on your prompts. Access is open to developers, enterprises, and Google AI Pro/Ultra subscribers with a 1M-token context window.

**「Community discussion」** Commenters focused largely on naming and positioning rather than independent technical validation: one complained that Google, Anthropic, and OpenAI now use too many model names to map easily to use cases, while another noted that Neon scores higher overall on the Artificial Analysis index but that Carbon remains positioned as the &quot;long-horizon&quot; model and scores higher on research-scale evals such as CritPt. A separate commenter reported Neon serving at 127 tokens per second through OpenRouter versus 46 for Carbon, and questioned that speed if Neon is meant to be the flagship model.

<details><summary>References</summary>
<ul>
<li><a href="https://artificialanalysis.ai/models/gemini-4-neon">Gemini 4 Neon: Intelligence, Performance &amp; Price Analysis</a></li>
<li><a href="https://deepmind.google/blog/introducing-gemini-4-neon/">Introducing Gemini 4 Neon - deepmind.google</a></li>

</ul>
</details>

**Tags**: `#Gemini 4 Neon`, `#Google AI`, `#large language models`, `#model releases`, `#AI benchmarking`

---

<a id="item-tech-news-2"></a>
### [Nginx HTTP/2 flaws enable unauthenticated worker code execution; fixes released](https://www.wiz.io/blog/nginx-http2-rce-vulnerabilities) ⭐️ 8.0/10

Nginx 1.30.7 and 1.31.9, released November 18, fix 10 CVEs; the release follows Xint&\#x27;s NGINX2Root disclosure of five Nginx flaws and a Linux kernel bug that the researchers say can be chained to go from an Nginx guest to host root. The central HTTP/2 issue, CVE-2026-123007, is a flow-control memory corruption that allows unauthenticated command execution inside an Nginx worker. Rapid7 has published a proof of concept, no in-the-wild exploitation has been reported, and operators who cannot upgrade are advised to disable externally facing HTTP/2.

hackernews · speedping · Nov 18, 15:19 · [Discussion](https://news.ycombinator.com/item?id=50547374)

**「How the flaw works」** The flaw is a heap buffer overflow in HTTP/2 flow-control handling: nginx can let the flow-control window exceed its permitted threshold, corrupting memory and typically crashing the worker \(tool-1-3\). It affects NGINX Plus and open-source configurations that use HTTP/2, and the fixes are in 1.31.9 and 1.30.7 \(tool-1-1, tool-1-2\).

**「Patch or disable HTTP/2」** Operators running affected nginx versions with HTTP/2 exposed should upgrade to 1.30.7 or 1.31.9; if they cannot, the stated fallback is to disable HTTP/2 on externally facing endpoints. The HTTP/2 flaw alone allows code execution in an nginx worker, while host-root compromise requires chaining five nginx bugs with a Linux kernel flaw, so patching closes both paths. A public Rapid7 proof-of-concept makes prompt patching advisable even though the source reports no in-the-wild exploitation yet; nginx is used by 29.7% of websites with a known web server, though only HTTP/2-enabled deployments are exposed to this vector.

**「Community discussion」** Commenters pushed back on the severity: one noted that HTTP/2 is not enabled by default in Nginx and that about 12% of servers use it, while another argued exploitation requires roughly 128 Gb of HTTP/2 traffic and specific CPU instructions, calling it a non-issue. A separate thread criticized disclosure timing, saying the fix appeared in the open-source repository a week before the advisory and that a simple &quot;disable HTTP/2&quot; PSA could have been issued sooner.

<details><summary>References</summary>
<ul>
<li><a href="https://cycode.com/blog/nginx2root-cve-2026-123007/">NGINX2Root (CVE-2026-123007): Affected Versions, How to Check ...</a></li>
<li><a href="https://access.redhat.com/security/cve/cve-2026-123007">CVE-2026-123007 - Red Hat Customer Portal</a></li>
<li><a href="https://nvd.nist.gov/vuln/detail/cve-2026-123007">NVD-CVE-2026-123007</a></li>
<li><a href="https://w3techs.com/technologies/details/ws-nginx">Usage Statistics and Market Share of Nginx, November 2026</a></li>

</ul>
</details>

**Tags**: `#nginx`, `#http2`, `#vulnerability`, `#remote-code-execution`, `#security`

---

<a id="item-tech-news-3"></a>
### [Microsoft Announces Seven AI Models at Ignite 2026](https://microsoft.ai/news/microsoft-ignite-2026/) ⭐️ 7.0/10

Microsoft announced seven new AI models, positioning the lineup around what it calls scalable price-performance. The announcement frames the release as a broad set of models competing on cost relative to capability rather than a single flagship launch. The supplied material does not name the individual models or give parameter counts, benchmark results, per-token pricing, or availability dates, so which models are generally available and to whom remains unconfirmed.

hackernews · gmays · Nov 18, 16:08 · [Discussion](https://news.ycombinator.com/item?id=50548021)

**「Background」** Microsoft&\#x27;s Ignite 2026 announcement covers seven models, with the pitch centered on scalable price-performance rather than a single flagship. Commenters single out MAI Code 2 for hands-on testing and describe Microsoft as positioning it alongside Anthropic&\#x27;s Opus and OpenAI&\#x27;s Sol, so the relevant comparison is not only capability but also the cost of running models in production.

**「Cheaper image-model option」** Organizations choosing models for image editing or high-volume generation get a cheaper benchmark candidate: Microsoft says MAI Image 2.7 ranks first on Artificial Analysis for image editing at one-fifth the price of GPT Image 2.6 Sunburst \(max\), with Image 2.7 Flash aimed at high-volume work. Buyers should treat the ranking and price comparison as Microsoft&\#x27;s claim and test output quality and total Azure costs on their own workloads before switching.

**「Community Discussion」** Commenter johnshahbazian reported testing MAI Code 2 for everyday work and called it &quot;quite good,&quot; saying he would not argue much with Microsoft&\#x27;s placement of it alongside Opus or Sol. ahmedfromtunis argued that Microsoft should release some models as open source or open weight if it hopes to win market share, warning it could otherwise repeat &quot;Windows Phone OS all over again,&quot; while athrowaway3z read the release as evidence that competitive pressure from Chinese models, OpenAI, and now Microsoft makes Anthropic&\#x27;s pricing hard to justify.

<details><summary>References</summary>
<ul>
<li><a href="https://microsoft.ai/news/microsoft-ignite-2026/">Seven new world-class models at scalable price-performance ...</a></li>
<li><a href="https://windowsforum.com/news/microsoft-ignite-2026-mai-code-2-models-agent-365-governance-and-enterprise-ai-stack.453003/">Microsoft Ignite 2026: MAI Code 2 Models, Agent 365 ...</a></li>

</ul>
</details>

**Tags**: `#Microsoft`, `#AI models`, `#price-performance`, `#MAI Code 2`, `#model competition`

---

<a id="item-tech-news-4"></a>
### [Google DeepMind&\#x27;s Genie 4 is available, but access terms remain unclear](https://blog.google/innovation-and-ai/models-and-research/google-deepmind/genie-4-now-available-project-genie/) ⭐️ 7.0/10

Google DeepMind announced that Genie 4, the next version of its world-model technology, is now available. The supplied announcement contains no technical details on capabilities, pricing, regional availability, or how Genie 4 differs from earlier versions. According to a commenter quoting the page, access is limited to &quot;Eligible Google AI Ultra subscribers,&quot; and the same commenter reports that their non-Workspace Google account still shows Genie 3 under Ultra, leaving it unclear whether the discrepancy is regional or a documentation lag.

hackernews · leumon · Nov 18, 18:49 · [Discussion](https://news.ycombinator.com/item?id=50550415)

**「Background」** Project Genie is the Google DeepMind product through which the Genie world models are offered, and Genie 4 is the next model in that line; coverage compares its editable worlds and audio with Genie 3. Access is rolling out inside Project Genie to eligible Google AI Ultra subscribers, with a waitlist for AI Pro, according to a report on the release.

**「Impact」** Prospective users outside the eligible Google AI Ultra subscriber group, including those on Workspace accounts, may be unable to access Genie 4 at launch, and at least one user reports that their Ultra account still lists Genie 3 rather than the new version. Would-be users should verify tier and regional eligibility before assuming access.

**「Community discussion」** Commenters focused on access and pricing confusion, with one noting that Google rarely makes it clear how to pay for its offerings and another reporting that their account still shows Genie 3 under Ultra. Others questioned whether generated worlds stay consistent when viewed from different angles—a commenter argued a true world must allow a 360° spin without details changing—and speculated about world models eventually serving as game engines, while one longtime reader said the pricing-and-capability framing left little room for discussing potential negative consequences.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.google/innovation-and-ai/models-and-research/google-deepmind/genie-4-now-available-project-genie/">Project Genie update featuring Genie 4 - The Keyword</a></li>
<li><a href="https://felloai.com/project-genie/">Project Genie: Genie 4 Access, Price and Limits - felloai.com</a></li>
<li><a href="https://www.online-tech-tips.com/google-genie-4-access-ai-ultra/">Google opens Genie 4 access to eligible AI Ultra subscribers</a></li>

</ul>
</details>

**Tags**: `#Genie 4`, `#Google DeepMind`, `#world models`, `#generative AI`, `#product launch`

---

<a id="item-tech-news-5"></a>
### [Quad9&\#x27;s France exit and the case against DNS piracy blocking](https://techstackups.com/articles/quad9-leaves-france-dns-blocking/) ⭐️ 7.0/10

Quad9 has withdrawn from France over the country&\#x27;s DNS-blocking regime, and a techstackups.com analysis argues that using public DNS resolvers as anti-piracy enforcement points is the wrong approach. The piece treats Quad9&\#x27;s exit as a case study in how blocking orders can remove a public resolver from a national market and turn basic infrastructure into a censorship chokepoint. It frames the issue as policy and opinion rather than a technical breakthrough; the available item does not detail the court order, scope, or timing.

hackernews · ritzaco · Nov 18, 13:18 · [Discussion](https://news.ycombinator.com/item?id=50545958)

**「Background」** Public DNS resolvers translate domain names into IP addresses, which is why rights holders have pushed courts to order blocking at that layer rather than pursuing individual sites or users. According to the Tech Stackups analysis, Quad9 — a Swiss non-profit recursive resolver — chose to stop serving users in France rather than comply with a court order requiring it to block domains associated with the sports broadcaster beIN Sports. Cloudflare&\#x27;s write-up on the same withdrawal argues the episode demonstrates the hazards of mandating DNS-level blocking.

**「Impact」** French users and network operators who relied on Quad9 lose a public resolver option and may need to switch to another provider. The article&\#x27;s concern is that DNS-level blocking also makes resolution decisions a censorship point that can affect domains beyond the pirated content.

**「Community Discussion」** Commenters offered competing fixes for piracy: one called non-prosecution anti-piracy efforts a backdoor to suppressing speech, while another argued that cheaper, DRM-free legal downloads would win paying users. Another commenter questioned whether blame belongs with judges applying the law or with lawmakers who wrote it, and a third argued enforcement is moot because AI companies have already consumed copyrighted material.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.cloudflare.com/quad9-withdrawal-from-france/">Quad 9 ’s withdrawal from France : A canary in the... | Cloudflare Blog</a></li>
<li><a href="https://techstackups.com/articles/quad9-leaves-france-dns-blocking/">Quad 9 Is Leaving France : Why DNS Resolvers Are... | Tech Stackups</a></li>

</ul>
</details>

**Tags**: `#DNS`, `#internet censorship`, `#privacy`, `#piracy policy`, `#internet infrastructure`

---

<a id="item-tech-news-6"></a>
### [From 4004 to 486: A Detailed x86 History](https://pikuma.com/blog/history-of-x86-4004-to-486) ⭐️ 7.0/10

This article is a detailed historical walkthrough of Intel&\#x27;s early x86 lineage, covering the 4004 through the 486 with architectural context. It is educational reading for systems and hardware enthusiasts rather than a report of a new release or benchmark.

hackernews · ibobev · Nov 18, 14:47 · [Discussion](https://news.ycombinator.com/item?id=50546967)

**「Background」** The article starts before x86 existed: the 4004 established Intel in the microprocessor business, and the 8008 followed in April 1972 as an 8-bit CPU with a 14-bit external address bus and 16 KB of addressable memory. Those early designs provide the pre-x86 context for the later chips covered in the walkthrough.

**「Community Discussion」** Commenters pushed back on several technical claims: one said little-endian ordering originally came from data-access speed on the 2200 rather than arithmetic, which became relevant with the 8080&\#x27;s 16-bit arithmetic, and that multiplexed address/data buses were not unique to the 8085. Others argued that the 8008 instruction set was not purely external because Intel engineers including Stan Mazor enhanced it, and that the 4004 and 8008 are unrelated apart from shared personnel.

<details><summary>References</summary>
<ul>
<li><a href="https://www.tomshardware.com/picturestory/710-history-of-intel-cpus.html">The History Of Intel CPUs: Updated! | Tom&#x27;s Hardware</a></li>
<li><a href="https://cpumuseum.jimdofree.com/museum/intel/8008/">Intel 8008 - CPU MUSEUM - MUSEUM OF MICROPROCESSORS...</a></li>

</ul>
</details>

**Tags**: `#x86 history`, `#CPU architecture`, `#Intel microprocessors`, `#computer history`, `#retrocomputing`

---

<a id="item-tech-news-7"></a>
### [Show HN: Interactive Voyager 1 tour reaches a single memory chip](https://rshekhar.com/voyager/) ⭐️ 7.0/10

A new Show HN interactive site at rshekhar.com/voyager lets readers explore Voyager 1’s hardware down to individual memory chips. The author says Voyager 1 reached one light-day from Earth and offers views of both probes’ current positions, the RTG’s 24 plutonium spheres, the data computer’s memory, a single command-computer memory bit, the Golden Record cover, the radio-repair story, and a live view of which Earth dish is listening. A four-minute film is also linked. It is an educational visualization, not a new mission result or a hardware change.

hackernews · raj-shekhar · Nov 18, 16:18 · [Discussion](https://news.ycombinator.com/item?id=50548161)

**「Background」** A light-day is the distance light travels in 24 hours, so Voyager 1&\#x27;s radio signals now take roughly a day each way, which is why the site&\#x27;s live view of Earth&\#x27;s listening dishes matters. The probe&\#x27;s computers were built from discrete memory chips rather than modern integrated modules, making it possible to navigate the visualization down to a single chip or bit — and meaning any repair, such as the one described on the site, has to be uploaded by radio rather than performed physically.

**「Impact」** For educators and spaceflight enthusiasts, the author’s direct links to the RTG, data-computer memory chips, a single command-computer bit, the Golden Record cover, and the repair story make the site usable as a guided reference rather than a linear article. The source presents no new measurements or verified failure analysis, so it is better suited to orientation and teaching than to authoritative engineering reference.

**「Community discussion」** Commenters praised the visualization; one shared a separate Golden Record tribute and an audio-to-image decoder, while another called the late-1970s engineering “pretty wild.” The sharper discussion questioned provenance and depth: one commenter asked whether the site was “vibecoded” and checked against authoritative sources, and another wanted the exact analog cause of the memory chip’s consistent misreads—such as charge-carrier erosion, thermal cycling, or a fractured package interconnect.

**Tags**: `#Voyager 1`, `#interactive visualization`, `#spacecraft computers`, `#hardware history`, `#memory chips`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Fed Minutes Signal More Rate Hikes, Flag AI Inflation Risks](https://www.cnbc.com/2026/11/18/fed-minutes-october-2026.html) ⭐️ 8.0/10

Federal Reserve meeting minutes released Wednesday showed almost all officials judged that further increases to the federal funds rate would likely be appropriate to bring inflation back to the 2% target, while the FOMC voted 10-2 to hold the benchmark rate at 3.75%-4%. The minutes also said officials saw AI-related demand as &quot;a material source of inflation risk&quot; and warned that rapid, opaque AI-related debt could amplify losses if returns disappoint.

rss · CNBC Finance · Nov 18, 19:41

**「Background」** The 3.75%-4% range the Fed held in October was set at its September 2026 meeting, when it approved its first rate hike since 2023, with officials then signaling another increase to come as they looked past inflation driven by Iran-war fuel costs and tariffs.

**「Who is exposed」** Fed staff warned that because much of the rapidly growing AI-related debt sits in off-balance-sheet leasing commitments and circular financing arrangements, losses could be amplified for the creditors and investors funding AI firms if returns on AI investment disappoint.

<details><summary>References</summary>
<ul>
<li><a href="https://www.cnbc.com/2026/09/16/fed-rate-decision-september-2026.html">Fed rate decision September 2026 : Rates rise to 3.75%-4%</a></li>
<li><a href="https://www.federalreserve.gov/monetarypolicy/files/fomcminutes20261028.pdf">Minutes of the Federal Open Market Committee - October 27-28, 2026</a></li>

</ul>
</details>

**Tags**: `#Federal Reserve`, `#monetary policy`, `#inflation`, `#interest rates`, `#AI financial risk`

---

<a id="item-finance-news-2"></a>
### [Tencent Q3: AI spending surges, capital expenditure well above forecasts](https://api3.cls.cn/share/article/2537922?os=android&amp;amp;sv=8.8.5&amp;amp;app=cailianpress&amp;amp;selected=) ⭐️ 8.0/10

Tencent reported 2026 third-quarter revenue of 207.3 billion yuan, up 8% year on year and below market expectations, with net profit attributable to shareholders of 63.6 billion yuan, up 0.8%. Capital expenditure reached 81.43 billion yuan against a market estimate of 55.4 billion yuan, pushing quarterly free cash flow to negative 69.1 billion yuan, while the company said its WorkBuddy app is China&\#x27;s most-used AI product by daily large-language-model token consumption at over 100 trillion tokens a day.

telegram · zaihuapd · Nov 18, 09:20

**「Background」** Tencent’s WorkBuddy, the product behind its token-usage claim, is a desktop AI agent for office tasks such as drafting reports and building spreadsheets. Capital expenditure is spending on long-term assets such as data centers and computing equipment, and free cash flow is the cash left after operating costs and such investment.

**「Impact」** The cash swing reflects Tencent funding AI infrastructure itself: operating cash flow of 2.6bn yuan was swamped by 65.1bn yuan of capital expenditure payments, including advance payments for computing capacity, so AI chip, server and data-centre suppliers are the direct beneficiaries while Tencent&\#x27;s own balance sheet absorbs the cost.

<details><summary>References</summary>
<ul>
<li><a href="https://www.workbuddy.ai/">WorkBuddy - AI Agent for Everyday Office Work</a></li>
<li><a href="https://www.developersdigest.tech/blog/tencent-workbuddy-explained-pricing-free-models-2026">Tencent WorkBuddy Explained: Pricing, Free Models, Verdict</a></li>
<li><a href="https://www.tencent.com/wp-content/uploads/2026/11/Tencent-Announces-2026-Third-Quarter-Results.pdf">For Immediate Release - Tencent</a></li>
<li><a href="https://finance.yahoo.com/technology/ai/articles/tencent-q3-revenue-misses-estimates-094554252.html?fr=sycsrp_catchall">Tencent Q3 revenue misses estimates as AI spending weighs on ...</a></li>

</ul>
</details>

**Tags**: `#Tencent`, `#earnings`, `#AI capex`, `#free cash flow`, `#China tech`

---

<a id="item-finance-news-3"></a>
### [Fed’s Waller calls for half-point rate hike in December](https://www.cnbc.com/2026/11/18/federal-reserve-governor-christopher-waller.html) ⭐️ 7.0/10

Federal Reserve Governor Christopher Waller said Wednesday the central bank may need a half-percentage-point rate hike at its Dec. 8-9 meeting to “shock people” and bring down inflation, which he said is worsening and most readings show above 3% versus the Fed’s 2% target. The call is Waller’s recommendation, not an FOMC decision, and other officials have favored more gradual tightening.

rss · CNBC Finance · Nov 18, 15:13

**「Background」** The Fed cut rates three times in 2025, began raising them in September and held steady in October; inflation reaccelerated this year after energy prices jumped following U.S. and Israeli strikes on Iran in late February.

**Tags**: `#Federal Reserve`, `#monetary policy`, `#interest rates`, `#inflation`

---

<a id="item-finance-news-4"></a>
### [Trump Arrives in Shenzhen for APEC Leaders&\#x27; Meeting](https://weibo.com/1699432410/5366644789744407) ⭐️ 7.0/10

US President Trump arrived at Shenzhen Bao&\#x27;an International Airport aboard his official aircraft and was greeted by Chinese President Xi Jinping, according to a repost of reports by state media Xinhua and CCTV. Trump is scheduled to attend the 33rd APEC informal leaders&\#x27; meeting, which the report says runs from November 18 to 19.

telegram · zaihuapd · Nov 18, 08:42

**「Background」** APEC is an annual forum for Asia-Pacific economies, and China is hosting this 33rd APEC Economic Leaders’ Meeting on Nov. 18–19.

<details><summary>References</summary>
<ul>
<li><a href="https://www.nine.com.au/world-news/donald-trump-arrives-in-china-for-xi-jinping-vladimir-putin-apec-summit-20261118-p61fex.html">APEC Summit: Albanese poses alongside Putin at... | Nine.com.au</a></li>

</ul>
</details>

**Tags**: `#US-China relations`, `#APEC`, `#summit diplomacy`, `#trade policy`

---

<a id="item-finance-news-5"></a>
### [China and South Korea announce substantive end to services, investment FTA talks](https://x.com/Jaemyung_Lee/status/2122988472994791476) ⭐️ 7.0/10

China and South Korea announced on Nov. 18 the substantive conclusion of follow-up negotiations to their free-trade agreement on services and investment. China committed most-favored-nation treatment for South Korean films and games and wider openings in tourism, legal, construction and finance, while both sides agreed to expand audiovisual co-production from films to TV dramas, animation, variety shows and documentaries; some technical matters remain for working-level talks.

telegram · zaihuapd · Nov 18, 10:02

**「Background」** The follow-up talks on services and investment began in March 2018 under the existing China–South Korea free trade agreement and had run for eight years and eight months, with Yonhap describing the announced “substantial conclusion” as the first such progress in that period.

<details><summary>References</summary>
<ul>
<li><a href="https://www.chosun.com/english/national-en/2026/11/19/NTPG5ZDJMBAKLH427BSO5LHJKU/">Korea-China FTA Service, Investment Negotiations ...</a></li>

</ul>
</details>

**Tags**: `#China-South Korea FTA`, `#services and investment`, `#trade policy`, `#cultural industries`, `#market access`

---

<a id="item-finance-news-6"></a>
### [China Proposes Scrapping New-Energy Vehicles With Their Batteries](https://wallstreetcn.com/articles/3786200) ⭐️ 7.0/10

China’s Commerce Ministry and eight other departments proposed on Nov. 17 revising scrapped-vehicle recycling rules to require new-energy vehicles to be dismantled together with their power batteries, and to study a digital ID system for those batteries; the policy is not final and detailed rules are still to be drafted.

telegram · zaihuapd · Nov 18, 12:22

**「Background」** Under an interim rule that took effect in April, a scrapped new-energy vehicle that arrives without its power battery is already treated as an incomplete vehicle; the proposed revision would add recycling-stage requirements and record each battery&\#x27;s flow.

**「Impact」** If adopted, the change would affect owners disposing of new-energy vehicles and recycling firms, which would need to keep the battery with the car and record its transfer.

**Tags**: `#新能源汽车`, `#动力电池回收`, `#报废汽车回收`, `#政策监管`, `#电池数字身份证`

---