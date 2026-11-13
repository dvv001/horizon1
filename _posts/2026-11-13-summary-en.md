---
layout: default
title: "Horizon Summary: 2026-11-13 (EN)"
date: 2026-11-13
lang: en
---

> From 44 items, 13 important content pieces were selected

---

**Technology News**
1. [smolmaxxing reports 16B LLMs on sub-1GB legacy devices](#item-tech-news-1) ⭐️ 8.0/10
2. [Chips and Cheese Interviews AMD&\#x27;s Mike Clark on Zen 6 Design](#item-tech-news-2) ⭐️ 8.0/10
3. [Rust 1.100 stabilizes never type, custom allocators, and Cargo dependency controls](#item-tech-news-3) ⭐️ 8.0/10
4. [Google announces Gemini 4 Hydrogen, an element-named Flash-tier model](#item-tech-news-4) ⭐️ 8.0/10
5. [Anthropic IPO discussion centers on unverified deal figures and AI lab economics](#item-tech-news-5) ⭐️ 8.0/10
6. [SemiAnalysis alleges Jensen Huang has left Nvidia amid GPU-smuggling claims](#item-tech-news-6) ⭐️ 8.0/10
7. [UMAP 0.6 adds recursive initialization and faster opt-in optimizers](#item-tech-news-7) ⭐️ 8.0/10
8. [US Commerce finalizing rule to curb Chinese remote AI chip access](#item-tech-news-8) ⭐️ 8.0/10
9. [PostgreSQL CVE-2026-6460: From 22-Year-Old Type Confusion to RCE](#item-tech-news-9) ⭐️ 7.0/10
10. [Independent audit: TRIBE v2 shows motion selectivity but no retinotopy or tonotopy](#item-tech-news-10) ⭐️ 7.0/10
11. [Apple details Secure Exclaves for audio/video isolation and recording-indicator checks](#item-tech-news-11) ⭐️ 7.0/10

**Financial News**
1. [China approves Eli Lilly&\#x27;s oral GLP-1 weight-loss drug](#item-finance-news-1) ⭐️ 8.0/10
2. [Fed Sets October 2027 Meeting Without Rate Vote](#item-finance-news-2) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [smolmaxxing reports 16B LLMs on sub-1GB legacy devices](https://github.com/hyperionaidev/smolmaxxing/) ⭐️ 8.0/10

The open-source smolmaxxing project has released custom kernels and modified model checkpoints aimed at running LLMs on very constrained legacy hardware. Its author reports 16B-parameter models running on a first-generation iPad Air and a Xiaomi TV box, each with less than 1GB of usable memory. The modified models are published on Hugging Face alongside results intended for reproduction. The reported memory use and speeds are self-reported and were not independently validated in the supplied material.

hackernews · mrashad74 · Nov 12, 15:23 · [Discussion](https://news.ycombinator.com/item?id=50468888)

**「Why sparse models fit in tiny memory budgets」** The work builds on sparse mixture-of-experts inference: only a fraction of a model&\#x27;s parameters are activated for any given token, so most weights can sit in flash storage instead of RAM. The project&\#x27;s own repository describes keeping only part of each model in memory and reading the remainder from flash as it is needed, which is the mechanism behind running 8B and 16B models in roughly 1 GB of RAM.

**「Impact」** Developers with similar old hardware can use the published kernels and Hugging Face checkpoints to attempt reproduction, but should benchmark memory use and throughput themselves before treating the reported speeds as deployment-ready.

**「Community discussion」** One commenter argued that modern coding agents have made much of the inference-porting work routine, leaving hardware sourcing and access as the main obstacles. Others welcomed the demoscene-style effort and pointed to rapid progress in small local models.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/hyperionaidev/smolmaxxing/">GitHub - hyperionaidev / smolmaxxing : maxxing the ability to run...</a></li>

</ul>
</details>

**Tags**: `#LLM inference`, `#edge devices`, `#legacy hardware`, `#custom kernels`, `#open source`

---

<a id="item-tech-news-2"></a>
### [Chips and Cheese Interviews AMD&\#x27;s Mike Clark on Zen 6 Design](https://chipsandcheese.com/p/talking-zen-6-with-mike-clark-at) ⭐️ 8.0/10

Chips and Cheese published an in-depth interview with AMD&\#x27;s Mike Clark focused on Zen 6 CPU design. The material available for this summary includes no specific architectural details, performance figures, product timelines, or availability information, so any concrete Zen 6 specifications cannot be verified from this source. The piece is a designer interview rather than a product announcement or an independently measured benchmark result.

hackernews · dverlaeckt80 · Nov 12, 14:12 · [Discussion](https://news.ycombinator.com/item?id=50467460)

**「Background」** Mike Clark, AMD&\#x27;s chief Zen architect, described the original Zen as a deliberate move away from AMD&\#x27;s stratified high-power and low-power CPU designs toward a single scalable architecture, a transition he called a challenge. In separate media sessions, Clark and AMD corporate vice president Madhu Rangarajan have also said Zen 6 was not designed specifically for agentic AI, responding to Nvidia and Arm positioning their data-center CPUs as purpose-built for that workload.

**「Community Discussion」** One Hacker News commenter, koutakun, called the article interesting and said it is &quot;very rare to see CPU designers go in depth,&quot; treating the technical candor of the discussion as the main draw rather than any disclosed specification.

<details><summary>References</summary>
<ul>
<li><a href="https://www.tomshardware.com/news/amd-zen-cpu-microarchitecture,32540.html">Everything Zen : AMD Presents New... | Tom&#x27;s Hardware</a></li>
<li><a href="https://mezha.net/eng/news/mezha-385a51640a816c08fe1be1d3_amd_executives_say/">AMD executives say Zen 6 was not designed specifically for... | Межа</a></li>

</ul>
</details>

**Tags**: `#AMD Zen 6`, `#CPU architecture`, `#hardware`, `#semiconductor`, `#technical interview`

---

<a id="item-tech-news-3"></a>
### [Rust 1.100 stabilizes never type, custom allocators, and Cargo dependency controls](https://blog.rust-lang.org/2026/11/12/Rust-1.100.0/) ⭐️ 8.0/10

Rust 1.100 has been released, and commenters highlight stabilizations of the never type and custom allocators for Rust developers, along with Cargo changes: a configurable minimum publish age \(RFC 3923\) that makes the resolver ignore versions newer than the configured threshold unless they are already in Cargo.lock, and cargo-install now using the lockfile in the .crate tarball by default, making --locked a no-op. Cargo also now warns about unused dependencies by default through cargo::unused\_dependencies, according to the discussion. The supplied item does not include the release notes, so these feature details rely on community reports; commenters add that APIs such as bool::toggle\(\), Box::map\(\), and str::trim\_prefix\(\)/trim\_suffix\(\) were stabilized but not mentioned in the blog post.

hackernews · mbStavola · Nov 12, 18:39 · [Discussion](https://news.ycombinator.com/item?id=50472038)

**「Background」** Rust 1.100.0 was released on November 12, 2026, after being branched from master on September 25, according to the release changelog, which also lists stabilization of the never type and \`extern &quot;custom&quot;\`. For Cargo, the new minimum-publish-age setting changes resolver behavior: when configured, it ignores crate versions newer than the configured age unless those versions are already recorded in \`Cargo.lock\`.

**「Impact」** For users installing binaries with cargo install, dependency versions now come from the lockfile shipped inside the .crate tarball rather than being resolved fresh, so installs may use older pinned versions and --locked no longer changes that behavior.

**「Community Discussion」** Commenters welcomed the release enthusiastically, with steveklabnik calling it &quot;a monumental release&quot; and nirinor listing the never type, custom allocators, and the Cargo changes as favorites; others pointed to stabilizations omitted from the blog post, such as bool::toggle\(\) and Box::map\(\). jadbox struck a skeptical note, asking whether compiler performance had improved and complaining about long compile times and large temporary-file buildup.

<details><summary>References</summary>
<ul>
<li><a href="https://releases.rs/docs/1.100.0/">1.100.0 | Rust Changelogs - releases.rs</a></li>
<li><a href="https://doc.rust-lang.org/nightly/releases.html">Rust Release Notes</a></li>

</ul>
</details>

**Tags**: `#rust`, `#programming-languages`, `#cargo`, `#memory-management`, `#supply-chain-security`

---

<a id="item-tech-news-4"></a>
### [Google announces Gemini 4 Hydrogen, an element-named Flash-tier model](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/) ⭐️ 8.0/10

Google published a blog post introducing Gemini 4 Hydrogen, the first model in a new &quot;Gemini 4&quot; generation, and users report it was swapped into the Gemini app immediately in place of 3.8 Flash. Beyond the title, the announcement text was not available for review, so benchmarks, context window, API identifiers, and regional availability remain unconfirmed. Commenters describe an element-based naming scheme \(Hydrogen, Argon\) applied to models that are meant to be compared against each other, and read Hydrogen as an entry-level model positioned to replace 3.5 Flash Lite. Several also claim it is priced at the same rate as non-discounted 3.8 Flash — above what they say they currently pay for Flash, Flash Lite, or older Gemini tiers — a figure not verified against Google&\#x27;s published price list.

hackernews · dvaplima · Nov 12, 18:01 · [Discussion](https://news.ycombinator.com/item?id=50471431)

**「Why the name changed」** Until this release, Google labeled the fast, cheaper end of its Gemini lineup with &quot;Flash&quot; and &quot;Flash Lite&quot; names — versions 3.8 Flash and 3.5 Flash Lite are the ones commenters describe being replaced. Coverage of the launch reports that Hydrogen follows this week&\#x27;s Gemini 4 Carbon and deliberately drops the &quot;Flash&quot; branding in favor of an element name, leaving the new model without an obvious slot in the old tier hierarchy; Google&\#x27;s post frames it as a standalone successor to 3.8 Flash rather than a like-for-like Flash refresh.

**「Impact」** If the pricing reported in the thread holds, teams that moved workloads onto Flash or Flash Lite to keep inference cheap would face a higher per-token cost on the replacement model, so checking the published price sheet and the model string in existing API calls before migrating is warranted. The element naming also complicates model selection, since Hydrogen and Argon give no inherent hint about relative capability or tier.

**「Community discussion」** The dominant complaint was the naming: one commenter who found 3.8 Flash silently replaced by &quot;4 Hydrogen&quot; argued that element names work for separate product lines but not for models users must rank against each other, noting that intuition would put Hydrogen above Argon. Others read Hydrogen&\#x27;s low atomic weight as a deliberate signal of an entry-level tier and questioned whether Google is abandoning its &quot;fast and cheap&quot; segment given the reported price. The thread also carried unrelated grievances about Gemini, including a claimed account suspension for command-line tool use and iPhone app reliability and integration gaps versus competing assistants.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/">Introducing Gemini 4 Hydrogen for Agentic Workflows</a></li>
<li><a href="https://9to5google.com/2026/11/12/gemini-4-hydrogen-launch/">Google announces Gemini 4 Hydrogen with ‘significant leaps&#x27;</a></li>

</ul>
</details>

**Tags**: `#Gemini`, `#Google`, `#LLM releases`, `#model pricing`, `#AI industry`

---

<a id="item-tech-news-5"></a>
### [Anthropic IPO discussion centers on unverified deal figures and AI lab economics](https://ipo.anthropic.com/us/) ⭐️ 8.0/10

A Hacker News item links to an Anthropic IPO page, and the discussion centers on deal terms that commenters say come from linked documents; the item itself supplies no document text. One commenter cites a $70–$78 price range, an $85.3B gross deal size including a $26B private placement, an implied market cap of about $968B at 13.09B shares, Q3 2026 revenue of $17.0B, roughly $81B run-rate revenue as of October 2026, $900.9B in compute commitments through 2045, and the ticker ANT on Nasdaq. Those figures are comment-derived and are not independently confirmed in the supplied material.

hackernews · josephljohnston · Nov 12, 11:46 · [Discussion](https://news.ycombinator.com/item?id=50465829)

**「Background」** Anthropic was valued at roughly $965 billion in its May 2026 funding round, and its amended S-1/A now sets a $70–$78 per-share range for 825 million shares on Nasdaq under the ticker ANT. That filing is the step before the shares can trade, with ShiftDelete reporting trading expected on Nov. 19, 2026.

**「Procurement risk」** The IPO filing discloses approximately $900.9 billion in compute and infrastructure commitments, with $451.6 billion expected by the end of 2030 and most of the remainder falling between 2031 and 2045. For organizations standardizing on Anthropic’s API, that makes contract length, rate-limit guarantees, and data-portability terms practical diligence items, because the vendor’s capacity obligations extend well beyond a typical procurement cycle.

**「Community discussion」** Commenters split on whether the IPO timing signals strength or capital need: one argued that if Anthropic&\#x27;s models were capable of recursive self-improvement, investors would have delayed the offering to secure clear market dominance, while another said LLM demand is easy to switch and frontier-model advantages may not protect lab economics. Others warned that improving local models could erode the moat and that late-stage private valuations could already be underwater at the low end of the cited range.

<details><summary>References</summary>
<ul>
<li><a href="https://www.gate.com/blog/gate-anthropic-ipo-valuation-subscription-and-outlook">Gate Anthropic IPO : Valuation , Subscription and Outlook | Gate Blog</a></li>
<li><a href="https://shiftdelete.net/en/anthropic-ipo-price-range">Anthropic IPO Price Range : $ 70 to $ 78 , Trading Eyed Nov . 19</a></li>
<li><a href="https://www.tipranks.com/news/amazon-and-google-could-win-big-as-anthropic-ipo-targets-411-billion-windfall-for-early-cloud-backers">Amazon and Google Eye $411 Billion in Combined Anthropic Shares...</a></li>
<li><a href="https://www.gate.com/news/detail/anthropic-commits-9009b-to-future-compute-and-infrastructure-spending-25532291">Anthropic Commits $900.9B to Future Compute and ...</a></li>
<li><a href="https://news.bloombergtax.com/financial-accounting/anthropic-ipo-filing-reveals-nearly-900-billion-in-future-debt">Anthropic IPO Filing Reveals Nearly $900 Billion in Future Debt</a></li>

</ul>
</details>

**Tags**: `#Anthropic`, `#AI industry`, `#IPO`, `#LLM economics`, `#Hacker News`

---

<a id="item-tech-news-6"></a>
### [SemiAnalysis alleges Jensen Huang has left Nvidia amid GPU-smuggling claims](https://newsletter.semianalysis.com/p/nvidia-and-the-world-without-jensen) ⭐️ 8.0/10

SemiAnalysis reported on 12 November that Jensen Huang is no longer Nvidia&\#x27;s CEO, writing that the board was investigating his conduct and that Colette Kress has been named interim CEO while the company seeks a permanent successor. The newsletter ties the exit, after 33 years at the helm, partly to what it says is large-scale diversion of export-restricted GPUs: its Accelerator Model data reportedly shows more than 1.5GW of restricted Nvidia chips ultimately reached China, a figure it says excludes the China-specific parts Nvidia designed to work around US rules. It further asserts that US intelligence pressure drove the departure and that RASA-style legislation, already passed by the House, will now advance faster, arguing the company has no deep successor bench behind Huang&\#x27;s roughly 60-direct-report structure. These are the outlet&\#x27;s own claims and analysis; the item offers no independent corroboration, and the Nvidia newsroom announcement it links to was not verified by any other source here.

rss · Semianalysis · Nov 12, 18:06

**「Context」** Huang had built an unusually flat management structure with roughly 60 direct reports and no publicly disclosed succession plan, leaving few obvious internal heirs. Nvidia named CFO Colette Kress as interim CEO while the board searches for a permanent successor.

**「Remote-access rules become the near-term exposure」** SemiAnalysis ties the leadership change to faster tightening of China chip rules, and the one concrete mechanism it names is already moving: the Remote Access Security Act, which passed the House in January 2026, would expand federal authority to restrict foreign adversaries&\#x27; access to AI chips remotely through cloud computing services. For cloud providers and developers who rent Nvidia capacity across borders instead of shipping hardware, region availability and licensing terms become the compliance item to plan around, not just export licenses on physical GPUs — the monitored remote-access channel SemiAnalysis argues is preferable to the smuggling it alleges.

**「Community discussion」** Hacker News commenters focused less on the reported conduct allegations than on timing and export controls: one argued the real question is &quot;why now&quot; and who benefits from surfacing the information, while another said the allegations matter chiefly through the perception of a CEO whose perceived stability the AI economy depends on. Another commenter said the substantive issue is whether Nvidia sold to China despite the export ban and that the reporting makes that hard to avoid concluding, and a further comment compared the situation to Sam Altman&\#x27;s brief ouster at OpenAI.

<details><summary>References</summary>
<ul>
<li><a href="https://wccftech.com/jensen-huang-resigns-nvidia-ceo-colette-kress-interim/">Jensen Huang Steps Down As NVIDIA CEO , As Company Thanks...</a></li>
<li><a href="https://finance.yahoo.com/technology/live/nvidia-live-updates-jensen-huang-resigns-cfo-colette-kress-to-serve-as-interim-ceo-140341430.html">Nvidia live updates: Jensen Huang resigns, CFO Colette Kress to...</a></li>
<li><a href="https://sanctionsnews.bakermckenzie.com/us-house-passes-remote-access-security-act/">US House Passes Remote Access Security Act</a></li>
<li><a href="https://chinaselectcommittee.house.gov/media/press-releases/house-passes-bipartisan-legislation-to-limit-adversaries-remote-access-to-critical-technology">House Passes Bipartisan Legislation to Limit Adversaries ...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#AI hardware`, `#export controls`, `#GPU smuggling`, `#semiconductor industry`

---

<a id="item-tech-news-7"></a>
### [UMAP 0.6 adds recursive initialization and faster opt-in optimizers](https://www.reddit.com/r/MachineLearning/comments/1xudaah/umap_06_new_initialization_new_optimizers_and/) ⭐️ 8.0/10

UMAP 0.6 is out with a new recursive initialization and new optimizers that the project author says make large-scale runs much faster and improve cluster detail; the claims have not been independently verified. The post reports roughly 4x faster nearest-neighbor search through better use of PyNNDescent, a 3-million-paper arXiv run finishing in under five minutes, and seeded runs that are reproducible while using every core; it says a seeded UMAP 0.5 run took 52 minutes single-threaded, 12 times longer. The initialization lays out a coarse graph with UMAP itself and refines it, while the optimizers add hard-negative mining and support higher repulsion strengths, yielding better kNN recall and finer structure in fewer epochs according to the author. The initialization and optimizers are opt-in because they change output: set compatibility\_layout=False; the author says future versions will make them the default, and installation is via pip install -U umap-learn or conda-forge.

reddit · r/MachineLearning · /u/lmcinnes · Nov 12, 13:51

**「Background」** UMAP is a non-linear dimensionality-reduction library. In version 0.5, seeded runs were single-threaded, initialization used spectral methods or PCA, and the optimizer was designed around a limited portion of the attraction-repulsion spectrum.

**「Impact」** Because the new initialization and optimizers change the embedding, users who enable compatibility\_layout=False should recheck downstream clusters, labels, and saved comparisons against UMAP 0.5 before adopting them; those who need existing behavior can leave the default until a future release changes it.

**Tags**: `#UMAP`, `#dimensionality reduction`, `#open source`, `#performance optimization`, `#machine learning`

---

<a id="item-tech-news-8"></a>
### [US Commerce finalizing rule to curb Chinese remote AI chip access](https://www.theinformation.com/articles/commerce-department-finalizing-long-awaited-ai-remote-access-rule) ⭐️ 8.0/10

The US Commerce Department is reportedly finalizing a rule that would bar Chinese AI companies from remotely using advanced AI chips through data centers outside China, with publication possible as early as this month. The measure would extend existing semiconductor export restrictions to seven countries, including Singapore, Malaysia, and Thailand, to close remote-access and chip-smuggling gaps, according to The Information. The rule is not yet final; Commerce is still consulting other government agencies.

telegram · zaihuapd · Nov 12, 03:42

**「Background」** Existing US semiconductor export controls restrict direct sales of advanced AI chips to China, but they do not cover Chinese firms renting compute capacity in third-country data centers. The reported rule would extend the Commerce Department&\#x27;s Bureau of Industry and Security controls to seven additional countries, including Malaysia, Singapore and Thailand, to close that remote-access route.

**「Impact」** If finalized, the rule would remove an overseas data-center route that Chinese AI companies could use to access advanced AI chips, extending US export-control exposure to cloud and data-center operators in the seven covered countries.

<details><summary>References</summary>
<ul>
<li><a href="https://www.theinformation.com/articles/commerce-department-finalizing-long-awaited-ai-remote-access-rule">Commerce Department Finalizing Long-Awaited AI Remote Access Rule</a></li>

</ul>
</details>

**Tags**: `#AI chip export controls`, `#US Commerce Department`, `#China AI`, `#Southeast Asia data centers`, `#semiconductor policy`

---

<a id="item-tech-news-9"></a>
### [PostgreSQL CVE-2026-6460: From 22-Year-Old Type Confusion to RCE](https://mehmetince.net/part-3-6-how-i-ended-up-turning-a-22-year-old-postgresql-type-confusion-primitive-into-rce-cve-2026-6460/) ⭐️ 7.0/10

A detailed technical write-up traces CVE-2026-6460, showing how a 22-year-old PostgreSQL type-confusion primitive was developed into remote code execution. The post walks through PostgreSQL internals and the exploitation path; it is vulnerability research rather than a vendor advisory or patch announcement.

hackernews · ozirus · Nov 12, 18:22 · [Discussion](https://news.ycombinator.com/item?id=50471761)

**「PostgreSQL&\#x27;s Datum type confusion」** PostgreSQL stores column values as a \`Datum\`, a machine word that can hold a small value directly or a pointer to the real data, paired with a separately stored type identifier. When the two disagree, the server can treat a pointer as an integer or vice versa, which is the type-confusion primitive behind CVE-2026-6460; PostgreSQL&\#x27;s advisory describes the flaw as allowing an object creator to execute arbitrary code as the operating system user running the database. The fix shipped in a security release that carried 52 CVEs in total, six of them tied to this research, with CVE-2026-6460 serving as the umbrella fix that introduces composite attribute versioning, and several of the batch scored CVSS 8.8.

**「Impact」** For PostgreSQL operators, the practical exposure question is whether exploitation requires an authenticated SQL session; if it does, CVE-2026-6460 is a privilege-escalation and tenant-isolation risk rather than an unauthenticated network compromise.

**「Community Discussion」** Commenters including logophobia and jmuguy argued that the described attacks look like SQL exploits requiring authenticated access, making them privilege escalation rather than RCE; logophobia said this mainly affects multi-tenant databases. Others, such as igbanam and sailfast, praised the post for sharing the exploitation path and PostgreSQL internals in detail.

<details><summary>References</summary>
<ul>
<li><a href="https://www.postgresql.org/support/security/CVE-2026-6460/">PostgreSQL : CVE - 2026 - 6460 : PostgreSQL type confusion after...</a></li>
<li><a href="https://mehmetince.net/part-3-6-how-i-ended-up-turning-a-22-year-old-postgresql-type-confusion-primitive-into-rce-cve-2026-6460/">Part 3/6 | How I Ended Up Turning a 22-Year-Old PostgreSQL ...</a></li>
<li><a href="https://www.phoronix.com/news/PostgreSQL-52-CVEs">PostgreSQL Sees New Releases For 52 Security... - Phoronix</a></li>

</ul>
</details>

**Tags**: `#PostgreSQL`, `#vulnerability research`, `#type confusion`, `#RCE`, `#database internals`

---

<a id="item-tech-news-10"></a>
### [Independent audit: TRIBE v2 shows motion selectivity but no retinotopy or tonotopy](https://www.reddit.com/r/MachineLearning/comments/1xuillf/does_metas_brainresponse_model_tribe_v2_actually/) ⭐️ 7.0/10

A solo, self-funded evaluation of Meta&\#x27;s TRIBE v2 brain-response model reports that it does not recover retinotopic \(d=0.05, n.s.\) or tonotopic \(ρ=-0.07, n.s., with loudness controlled\) maps when run on classic mapping stimuli — checkerboard wedges and rings, hemifield flicker, moving dots, and tone sweeps — with the same analysis models used on real fMRI. Motion selectivity, by contrast, was sharp and localized to MT+ \(d=4.31, a 52x enrichment over chance\). The author points out that TRIBE v2&\#x27;s paper never tested these topographic maps and that its methods spatially average video features before prediction, which should destroy position information. An eccentricity effect that was null by default turned significant and &quot;correct&quot; under three separate stimulus-geometry controls, which the author interprets as an image-statistics confound rather than a positional code. The work is single-author, not peer reviewed or replicated; code and a write-up are posted at jakubstrawa1.github.io/audit-multimodal-brain-response.

reddit · r/MachineLearning · /u/Own\_Tank1283 · Nov 12, 17:16

**「Background」** TRIBE v2 is Meta&\#x27;s deep multimodal brain-encoding model that predicts fMRI responses to video, audio, and text by mapping multimodal representations onto the cortical surface. It follows the earlier TRIBE model, described as the first deep network trained to predict brain responses across modalities, cortical areas, and individuals. The independent audit tested whether TRIBE v2 reproduces classic topographic maps—retinotopy for visual-field position and tonotopy for sound frequency—although the model&\#x27;s paper did not test these, and its methods spatially average video features before prediction, which the poster argues should degrade position information.

**「What it means for users of the model」** For researchers treating TRIBE v2 predictions as a stand-in for visual-cortex response, the results argue against reading retinotopic or tonotopic organization out of the model, while its MT+ motion response may still be usable. The author&\#x27;s eccentricity result also implies that any positional effect recovered from such models needs stimulus-geometry controls before it is accepted.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/facebookresearch/tribev2">GitHub - facebookresearch/tribev2: This repository contains ...</a></li>
<li><a href="https://arxiv.org/abs/2507.22229">[2507.22229] TRIBE: TRImodal Brain Encoder for whole-brain ...</a></li>

</ul>
</details>

**Tags**: `#neuroimaging`, `#fMRI`, `#model evaluation`, `#reproducibility`, `#TRIBE v2`

---

<a id="item-tech-news-11"></a>
### [Apple details Secure Exclaves for audio/video isolation and recording-indicator checks](https://security.apple.com/blog/secure-exclaves/) ⭐️ 7.0/10

According to a Telegram tech-channel summary of Apple&\#x27;s Nov. 12 post, Secure Exclaves processes audio and video in a separate secure environment so the main system and apps in ambient-awareness mode receive only required recognition results rather than raw data. The architecture is used for HomeView face and sound recognition and for the iPhone 18 Pro privacy indicator. On the iPhone 18 Pro, dedicated hardware verifies the microphone indicator dot&\#x27;s color, brightness, and visibility before audio is allowed into the main system; Apple also requires the dot to remain displayed during relevant Siri audio sessions for at least three seconds total to prevent occlusion or spoofing.

telegram · zaihuapd · Nov 12, 09:13

**「Background」** Apple&\#x27;s post describes Secure Exclaves as protected, compartmentalized runtimes for camera and microphone data, with isolation features built into multiple silicon components to keep those runtimes separate from the rest of the system. MacRumors reports Apple applied the design to HomeView and iPhone 18 Pro, while AndroidPure&\#x27;s summary says the iPhone 18 Pro, Pro Max and Duo verify the mic or camera indicator before releasing full audio or video to apps or Siri.

**「Impact」** For developers of ambient-awareness features, Apple&\#x27;s stated design limits apps to recognition outputs instead of raw audio or video, reducing the data they can access while also constraining what they can process themselves.

<details><summary>References</summary>
<ul>
<li><a href="https://security.apple.com/blog/secure-exclaves">Secure Exclaves and Ambient Sensing - Apple Security Research</a></li>
<li><a href="https://www.macrumors.com/2026/11/12/apple-homeview-secure-exclaves/">Apple Explains How HomeView Keeps Camera Data Private</a></li>
<li><a href="https://www.androidpure.com/apple-secure-exclaves-iphone-18-pro-mic-indicator/">Apple Says iPhone 18 Pro Holds Hey Siri Audio Until the Mic ...</a></li>

</ul>
</details>

**Tags**: `#security architecture`, `#privacy`, `#Apple`, `#hardware security`, `#audio/video`

---

## Financial News

<a id="item-finance-news-1"></a>
### [China approves Eli Lilly&\#x27;s oral GLP-1 weight-loss drug](https://www.reuters.com/business/healthcare-pharmaceuticals/china-approves-eli-lillys-weight-loss-pill-orforglipron-2026-11-12/) ⭐️ 8.0/10

China approved Eli Lilly&\#x27;s once-daily oral GLP-1 weight-loss drug orforglipron, sold as 穆优达, on Nov. 12 for adults with obesity or overweight plus at least one weight-related comorbidity, making it the country&\#x27;s first approved oral GLP-1 weight-loss medicine; price and launch date were not disclosed.

telegram · zaihuapd · Nov 12, 10:09

**「Background」** Orforglipron was approved in the U.S. as Foundayo in April 2026 for adults with obesity or overweight plus weight-related medical problems \(tool-1-1\). Until this approval, the GLP-1 weight-loss drugs it competes with in China were given as weekly injections, so patients now have a once-daily pill option.

**「Impact」** The approval gives adults with obesity or overweight plus at least one weight-related condition a once-daily oral option alongside weekly injections, though the undisclosed price and launch timing leave patient access uncertain.

<details><summary>References</summary>
<ul>
<li><a href="https://investor.lilly.com/news-releases/news-release-details/fda-approves-lillys-foundayotm-orforglipron-only-glp-1-pill">FDA approves Lilly&#x27;s Foundayo™ (orforglipron), the only GLP-1 ...</a></li>

</ul>
</details>

**Tags**: `#礼来`, `#口服GLP-1`, `#减重药`, `#中国药监局批准`, `#肥胖治疗市场`

---

<a id="item-finance-news-2"></a>
### [Fed Sets October 2027 Meeting Without Rate Vote](https://www.cnbc.com/2026/11/12/in-policy-switch-fed-says-its-october-2027-meeting-will-not-see-a-vote-on-interest-rates.html) ⭐️ 7.0/10

The Federal Reserve said its October 26-27, 2027, policy meeting will not include a vote on interest rates, instead reserving the session for broad monetary-policy strategy as part of Chairman Kevin Warsh&\#x27;s push to streamline communication. The 2027 calendar has seven voting meetings, down from the Fed&\#x27;s usual eight, and the year&\#x27;s final meeting moves to November from December.

rss · CNBC Finance · Nov 12, 19:05

**「Background」** The Fed normally meets eight times a year and holds a rate vote and a chair&\#x27;s news conference after each meeting; since Warsh took over, post-meeting statements have been shortened and press sessions cut to about half an hour from roughly 45 minutes.

**Tags**: `#Federal Reserve`, `#monetary policy`, `#FOMC`, `#central bank communication`, `#meeting schedule`

---