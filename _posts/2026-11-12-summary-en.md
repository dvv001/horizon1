---
layout: default
title: "Horizon Summary: 2026-11-12 (EN)"
date: 2026-11-12
lang: en
---

> From 42 items, 15 important content pieces were selected

---

**Technology News**
1. [Reports of Jensen Huang&\#x27;s Nvidia resignation remain unconfirmed](#item-tech-news-1) ⭐️ 8.0/10
2. [Rust 1.100.0 released with never type, custom allocators, Cargo cooldowns](#item-tech-news-2) ⭐️ 8.0/10
3. [Google announces Gemini 4 Hydrogen, drawing naming and pricing questions](#item-tech-news-3) ⭐️ 8.0/10
4. [Anthropic IPO page draws debate over valuation and open weights](#item-tech-news-4) ⭐️ 8.0/10
5. [AWS ships Rust-based local emulator for its services](#item-tech-news-5) ⭐️ 8.0/10
6. [UMAP 0.6 adds recursive initialization and new optimizers, claims large speedups](#item-tech-news-6) ⭐️ 8.0/10
7. [US Commerce Department Reportedly Finalizing Chinese AI Chip Remote-Access Rule](#item-tech-news-7) ⭐️ 8.0/10
8. [smolmaxxing claims 16B LLM inference on sub-1GB devices](#item-tech-news-8) ⭐️ 7.0/10
9. [Microsoft 365 connectivity outage reported; status page unavailable](#item-tech-news-9) ⭐️ 7.0/10
10. [Why Writing Correct Software Is Hard: Formal-Methods Debate](#item-tech-news-10) ⭐️ 7.0/10
11. [Google launches Gemini Decision 1 decisions API with multimodal inputs](#item-tech-news-11) ⭐️ 7.0/10
12. [Audit finds TRIBE v2 lacks retinotopic and tonotopic maps but shows MT+ selectivity](#item-tech-news-12) ⭐️ 7.0/10

**Technology Blog**
1. [vLLM-Omni Brings MiniMax H3-Image to Vera Rubin](#item-tech-blog-1) ⭐️ 7.0/10

**Financial News**
1. [礼来口服减重药在中国获批，为国内首个口服GLP-1减重药](#item-finance-news-1) ⭐️ 8.0/10
2. [Fed to Skip Rate Vote at October 2027 Meeting](#item-finance-news-2) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Reports of Jensen Huang&\#x27;s Nvidia resignation remain unconfirmed](https://apnews.com/article/nvidia-megaspeed-china-singapore-huang-5403f152a601cf82ce939f1d24fffa0f) ⭐️ 8.0/10

Discussion links point to reports that Nvidia CEO Jensen Huang has resigned, but the submitted material contains only truncated URLs and headlines, so the effective date, the board&\#x27;s stated reason, and any named successor cannot be confirmed from the available evidence. Commenters split over whether the departure is tied to Nvidia&\#x27;s China sales, with some alleging the company evaded export controls and others countering that recent sales were approved by the U.S. government. The resignation itself and its cause should be treated as unverified until the full announcements and article text are available.

hackernews · lldb · Nov 12, 13:52 · [Discussion](https://news.ycombinator.com/item?id=50467087)

**「Background」** The departure followed reports that Huang had been involved with a woman identified by U.S. intelligence as a Chinese spy, as well as with a company employee; The Guardian reported those affairs as the trigger for his resignation. Nvidia&\#x27;s board announced on November 12, 2026, that Huang had resigned as president, CEO, and board member effective immediately, with CFO Colette Kress taking over on an interim basis.

**「Export-control fallout」** The reported resignation has already prompted the House Select Committee on China, led by Republican Rep. John Moolenaar, to call for stronger chip export controls, so Nvidia and its customers face a more restrictive compliance environment.

**「Community discussion」** One commenter argued that the export ban exists for national-security reasons regardless of whether one agrees with it, and said the reporting led them to conclude that &quot;NVIDIA sold to China despite the export ban,&quot; while another countered that the sales were &quot;done legally with the US government taking a cut&quot; and that criticism should fall on U.S. policy instead. Others focused on Huang&\#x27;s record of shareholder value and employee stock compensation, and one said the appearance of impropriety alone had left him &quot;compromised&quot; — these are commenter opinions, not established facts.

<details><summary>References</summary>
<ul>
<li><a href="https://www.theguardian.com/technology/2026/nov/12/nvidia-ceo-jensen-huang-resigns">Jensen Huang resigns as Nvidia CEO after alleged... | The Guardian</a></li>
<li><a href="https://www.nytimes.com/live/2026/11/12/business/nvidia-jensen-huang-resigns">Jensen Huang Resigns as Nvidia CEO After Affairs: Live Updates</a></li>
<li><a href="https://nvidianews.nvidia.com/news/nvidia-announces-ceo-transition">NVIDIA Announces CEO Transition | NVIDIA Newsroom</a></li>
<li><a href="https://www.voanews.com/a/nvidia-ceo-jensen-huang-resigns-as-us-lawmakers-push-tougher-chip-export-controls/8222967.html">Nvidia CEO Jensen Huang resigns as US lawmakers push tougher ...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#AI hardware`, `#export controls`, `#semiconductor industry`, `#corporate leadership`

---

<a id="item-tech-news-2"></a>
### [Rust 1.100.0 released with never type, custom allocators, Cargo cooldowns](https://github.com/rust-lang/rust/releases/tag/1.100.0) ⭐️ 8.0/10

Rust 1.100.0 has been released, and commenters point to the official release blog post as the better summary of its changes. They highlight stabilization of the never type and custom allocators, plus a Cargo minimum publish age setting \(RFC 3923, \#17335\) that makes the resolver ignore versions published more recently than the configured age unless they are already in Cargo.lock. The same comment notes that cargo install now uses the lockfile inside the .crate tarball by default, making --locked a no-op \(\#17388\). Another commenter lists stabilized APIs the blog post did not mention, including bool::toggle\(\), Box::map\(\), and str::trim\_prefix\(\)/trim\_suffix\(\).

hackernews · thesuperbigfrog · Nov 12, 18:24 · [Discussion](https://news.ycombinator.com/item?id=50471793)

**「Background」** The dependency-cooldown setting comes from RFC 3923, a proposal dated Feb. 23, 2026, that added a Cargo option specifying a minimum age for registry crate versions, with an override for exceptions such as urgent security fixes \[tool-2-1\]\[tool-2-2\]. The RFC was stabilized in rust-lang/cargo\#17335 and was expected to ship in Rust 1.100 on Nov. 12, 2026 \[tool-2-3\].

**「Impact」** Rust developers using the never type or custom allocators can move that code off nightly feature gates, and Cargo users can opt into dependency cooldowns through the new publish-age configuration. The cargo install change alters existing behavior: --locked no longer affects resolution, so scripts and CI workflows that depend on it should be reviewed.

**「Community discussion」** Commenters describe the release as unusually large, with ammar\_az noting that useful stabilizations such as bool::toggle\(\) and Box::map\(\) did not even make the blog post. jadbox asked whether compiler performance has improved and reported running cargo clean daily to remove roughly 90 GB of temporary files; no supplied reply addresses that complaint.

<details><summary>References</summary>
<ul>
<li><a href="https://rust-lang.github.io/rfcs//3923-cargo-min-publish-age.html">3923-cargo-min-publish-age - The Rust RFC Book</a></li>
<li><a href="https://github.com/rust-lang/rfcs/blob/master/text/3923-cargo-min-publish-age.md">rfcs/text/3923-cargo-min-publish-age.md at main · rust-lang ...</a></li>
<li><a href="https://github.com/Michael-Dahlke/cyber-news-tool/issues/22">Enable Cargo min-publish-age cooldown once Rust 1. ... - GitHub</a></li>

</ul>
</details>

**Tags**: `#Rust`, `#programming languages`, `#Cargo`, `#compiler tooling`, `#language features`

---

<a id="item-tech-news-3"></a>
### [Google announces Gemini 4 Hydrogen, drawing naming and pricing questions](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/) ⭐️ 8.0/10

Google announced Gemini 4 Hydrogen, and Hacker News commenters reported that it was rolled out immediately in the Gemini app in place of 3.8 Flash. The supplied material includes no official specifications, benchmark results, availability details, or confirmed pricing. Commenters said the element-based name makes model comparison harder and debated whether Hydrogen is an entry-level replacement priced at the non-discounted 3.8 Flash rate, a positioning inference rather than a verified vendor statement.

hackernews · dvaplima · Nov 12, 18:01 · [Discussion](https://news.ycombinator.com/item?id=50471431)

**「Background」** Commenters are comparing Gemini 4 Hydrogen with earlier Gemini releases labeled 3.8 Flash and 3.5 Flash Lite, so the element-based name breaks the versioned Flash convention they were using to judge capability and price. Google&\#x27;s announcement describes Hydrogen as a fast, cost-efficient model for agentic workflows \[tool-2-1\]. Third-party trackers list API pricing of $1.50 per million input tokens and $7.50 per million output tokens \[tool-2-2\].

**「Cost check before switching」** Developers using Gemini 3.8 Flash face a migration decision: Gemini 4 Hydrogen is reported to run 2.5x faster and list at $1.50 per million input tokens, but a commenter says that price matches non-discounted 3.8 Flash and is well above current discounted rates. Cost-sensitive workloads should verify their actual billed rate before switching.

**「Community discussion」** Commenters focused on the element-based naming, with one saying it is unclear whether Hydrogen or Argon should be more capable, and on whether Google is abandoning its fast-and-cheap tier, based on one commenter&\#x27;s reading that Hydrogen is priced at the non-discounted 3.8 Flash rate. A separate thread raised Gemini app reliability on iPhone and missing integration with other Google AI tools, while another commenter expected a near-frontier free default to raise perceived AI capability for the general public.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/">Introducing Gemini 4 Hydrogen for Agentic Workflows</a></li>
<li><a href="https://artificialanalysis.ai/models/gemini-4-hydrogen">Gemini 4 Hydrogen (xhigh) - Intelligence, Performance &amp; Price Analysis</a></li>
<li><a href="https://cryptobriefing.com/gemini-4-hydrogen-faster-than-3-8-flash/">Google&#x27;s Gemini 4 Hydrogen runs 2.5x faster than 3.8 Flash ...</a></li>

</ul>
</details>

**Tags**: `#Gemini`, `#large language models`, `#AI model release`, `#model naming`, `#pricing`

---

<a id="item-tech-news-4"></a>
### [Anthropic IPO page draws debate over valuation and open weights](https://ipo.anthropic.com/us/) ⭐️ 8.0/10

Anthropic&\#x27;s IPO page drew a Hacker News discussion on Nov. 12, 2026, giving prospective investors and AI-industry watchers a set of commenter-cited terms rather than verified article detail. A commenter summarizing the linked documents lists a $70–$78 price range, an $85.3B gross deal including a $26B private placement, an implied market cap of about $968B at $74, Q3 2026 revenue of $17.0B, and a roughly $81B run rate as of October 2026. The same comment cites $900.9B in compute commitments through 2045 and the Nasdaq ticker ANT.

hackernews · josephljohnston · Nov 12, 11:46 · [Discussion](https://news.ycombinator.com/item?id=50465829)

**「Background」** Anthropic&\#x27;s IPO follows an October 2026 filing that disclosed rapid revenue growth alongside large losses, while leaving the share count and IPO price range undisclosed at that point, according to FXStreet&\#x27;s account of the filing. The New York Times reported on Oct. 14, 2026, that Anthropic&\#x27;s third-quarter revenue rose 45% to $16.8 billion and that the offering could value the company at $2 trillion, with trading expected at that time to begin as early as the following month.

**「Impact」** For organizations evaluating Anthropic, the cited $900.9B compute commitment through 2045 creates a diligence question about whether premium frontier-model demand can persist for years while open-weight alternatives remain only months behind, making multi-provider portability a practical procurement safeguard.

**「Community discussion」** Commenters split on whether the IPO timing signals strength or a need for capital: maerF0x0 argued that if Anthropic&\#x27;s models were good enough for recursive self-improvement, investors would have delayed the listing rather than accept dilution for $100B today. QuantumNoodle and maupin countered that open-weight and local models are only a few months behind at far lower cost, while brainless said most applications do not need frontier models and users can switch easily.

<details><summary>References</summary>
<ul>
<li><a href="https://www.fxstreet.com/news/anthropic-ipo-filing-reveals-rapid-growth-as-investors-weigh-an-80-billion-loss-202610270748">Anthropic IPO filing reveals rapid growth as investors weigh an $80...</a></li>
<li><a href="https://www.nytimes.com/2026/10/14/technology/anthropic-ipo-revenue-profit.html">Anthropic Says Revenue Jumped 45% to $16.8 Billion in Third Quarter</a></li>

</ul>
</details>

**Tags**: `#Anthropic`, `#IPO`, `#AI industry`, `#frontier models`, `#open-weight models`

---

<a id="item-tech-news-5"></a>
### [AWS ships Rust-based local emulator for its services](https://simonwillison.net/2026/Nov/11/aws-emulator/) ⭐️ 8.0/10

AWS has released aws-emulator, an official tool for running tests against local clones of its services without provisioning a paid API key. It is written in Rust, and Simon Willison notes the repository accumulated 29,684 commits in the project&\#x27;s first three weeks, with Swaminathan Sivasubramanian describing its AI-agent-driven development in a guest post on Werner Vogels&\#x27; blog. On macOS and Windows it currently requires Docker to run; Willison hopes for a single downloadable binary usable in test suites across other languages and platforms.

rss · Simon Willison · Nov 11, 21:18

**「Why it matters」** Local emulation of cloud services is a common testing pattern, but AWS had not previously offered an official emulator, leaving developers to provision real resources or rely on third-party mimics. The aws-emulator release changes that by providing a first-party local clone for tests.

**「For developers」** Teams testing against AWS APIs can now point test suites at a local clone instead of paid cloud resources or third-party emulators. The Docker dependency on macOS and Windows is a current constraint for CI setups and for developers wanting a drop-in binary in non-containerized test runs.

**Tags**: `#AWS`, `#local emulator`, `#software testing`, `#AI coding agents`, `#Rust`

---

<a id="item-tech-news-6"></a>
### [UMAP 0.6 adds recursive initialization and new optimizers, claims large speedups](https://www.reddit.com/r/MachineLearning/comments/1xudaah/umap_06_new_initialization_new_optimizers_and/) ⭐️ 8.0/10

UMAP 0.6, announced by the library&\#x27;s author, adds a recursive initialization that lays out a coarse version of the graph using UMAP itself and then refines it, plus new optimizers built on hard-negative mining and better handling of high repulsion strengths; the author says this resolves finer cluster structure in fewer epochs and gives better kNN recall. Nearest-neighbor search is reported about 4x faster through better use of PyNNDescent, and seeded runs are now reproducible while using every core; on 3 million arXiv papers the author reports a full run finishing in under five minutes, versus 52 minutes for a seeded 0.5 run he describes as single-threaded. The new initialization and optimizers change the output and remain opt-in via compatibility\_layout=False, with future versions planned to make them the default; the release installs with pip install -U umap-learn and is also on conda-forge. The performance and quality figures come from the author&\#x27;s own benchmarks and demo videos, not independent testing.

reddit · r/MachineLearning · /u/lmcinnes · Nov 12, 13:51

**「Background」** UMAP is a dimensionality-reduction library that lays out high-dimensional data in a lower-dimensional embedding. According to the release post, earlier versions initialized with spectral methods or PCA and optimized within a narrower portion of the attraction–repulsion range, which constrained behavior at large scale.

**「Impact」** Because the new initialization and optimizers alter the layout, teams that depend on reproducible embeddings from UMAP 0.5 should either pin umap-learn to 0.5 or set compatibility\_layout=False deliberately and re-validate downstream clustering or visualization steps. The advertised speed and fidelity gains only apply when that flag is enabled, since the defaults still use the older behavior.

**Tags**: `#dimensionality-reduction`, `#umap`, `#machine-learning`, `#performance`, `#open-source`

---

<a id="item-tech-news-7"></a>
### [US Commerce Department Reportedly Finalizing Chinese AI Chip Remote-Access Rule](https://www.theinformation.com/articles/commerce-department-finalizing-long-awaited-ai-remote-access-rule) ⭐️ 8.0/10

The US Commerce Department is reportedly finalizing a rule that would block Chinese AI companies from remotely using advanced AI chips through overseas data centers, with publication possible as early as this month. The reported rule would extend existing semiconductor export restrictions to Malaysia, Singapore, Thailand and four other countries, aiming to close remote-access and chip-smuggling gaps. The department is consulting other government agencies before finalizing the rule; the White House has previously asked Congress to legislate the requirement for Commerce to write it, and Nvidia has lobbied against closing the remote-access loophole.

telegram · zaihuapd · Nov 12, 03:42

**「Background」** The reported rule builds on existing US semiconductor export restrictions, which have primarily governed physical chip shipments rather than computing capacity accessed remotely through overseas data centers. According to the source, the White House had asked Congress to legislate and direct the Commerce Department to draft such a rule; Nvidia lobbied against closing the remote-access route.

**「Impact」** If finalized as reported, the plan would place data-center operators in Malaysia, Singapore, Thailand, and four other added countries on a license list with end-user reporting requirements for advanced AI chips, raising the compliance burden on cross-border compute arrangements. Chinese AI developers that have signed agreements for overseas data-center capacity, including Tencent, Alibaba, and ByteDance, could need to document, renegotiate, or relocate those workloads.

<details><summary>References</summary>
<ul>
<li><a href="https://biz.chosun.com/en/en-international/2026/11/12/M2ICNVHJPVCFLJDLAGG5IP4VDE/">US to widen AI chip export controls to seven nations, curb ...</a></li>
<li><a href="https://www.gate.com/news/detail/NVDA/us-prepares-ai-chip-export-controls-targeting-7-countries-to-block-china-25571564">US Prepares AI Chip Export Controls Targeting 7 Countries to ...</a></li>

</ul>
</details>

**Tags**: `#AI chips`, `#export controls`, `#US-China tech policy`, `#semiconductor industry`, `#data centers`

---

<a id="item-tech-news-8"></a>
### [smolmaxxing claims 16B LLM inference on sub-1GB devices](https://github.com/hyperionaidev/smolmaxxing/) ⭐️ 7.0/10

The open-source smolmaxxing project has released kernels and modified Hugging Face model weights that its author says allow 16B-parameter LLMs to run on an iPad Air 1st gen and a Xiaomi TV box, both with less than 1GB of usable memory. The author also claims &quot;some decent speeds,&quot; but the supplied material provides no tokens-per-second figures, memory measurements, or independent benchmarks, so the results remain unverified.

hackernews · mrashad74 · Nov 12, 15:23 · [Discussion](https://news.ycombinator.com/item?id=50468888)

**「Background」** smolmaxxing targets commodity devices with very little usable memory; its repository cites a Xiaomi TV Box S \(3rd Gen\) with an Amlogic S7D, four Cortex-A55 cores at 2.5 GHz, 1.9 GB of RAM \(about 1 GB usable\), and Android 14 without root. The project says it runs models from 260K to 16B parameters on that box, although another repository page and the project&\#x27;s product page list a 9B ceiling, so the published model range is not yet consistent. It also releases the kernels and modified models for reproduction.

**「Reproduction, not yet a deployment target」** Because the author released the kernels and modified Hugging Face weights, edge-AI developers can attempt the setup on their own sub-1GB devices. The 16B-model result is still an early, single-source report, so teams should measure actual peak memory and tokens per second on their target hardware before treating it as a deployable configuration.

**「Community discussion」** Commenters were interested but questioned the practical value: one asked whether small models are &quot;smart enough to be useful on practical tasks,&quot; while another described work on an LLM compressed to 970 KB. A separate commenter argued that modern coding agents can already handle much of the porting work, making access to old hardware the harder constraint.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/hyperionaidev/smolmaxxing">GitHub - hyperionaidev/smolmaxxing: maxxing the ability to ...</a></li>
<li><a href="https://github.com/hyperionaidev/smolmaxxing/tree/main">GitHub - hyperionaidev/smolmaxxing: maxxing the ability to ...</a></li>
<li><a href="https://hyperion-ai.com/products/smolmaxxing">smolmaxxing — The biggest model on the smallest hardware ...</a></li>

</ul>
</details>

**Tags**: `#LLM inference`, `#edge computing`, `#model optimization`, `#open source`, `#low-resource hardware`

---

<a id="item-tech-news-9"></a>
### [Microsoft 365 connectivity outage reported; status page unavailable](https://news.ycombinator.com/item?id=50471668) ⭐️ 7.0/10

A Hacker News user reported that all of their organization&\#x27;s Microsoft Cloud connections went down and that Microsoft&\#x27;s status page would not load, prompting others to share similar experiences. Status updates quoted in the thread said Microsoft was investigating an issue affecting multiple Microsoft 365 services, with affected infrastructure experiencing elevated load across multiple regions; the company was restarting and repairing impacted portions and testing a configuration change. A 7:52 PM UTC update quoted in the discussion said affected servers were failing automated health checks and that this may be related to a recent change to a component involved in processing those checks. The reports were crowd-sourced and developing, and the source did not establish the full scope or a recovery time.

hackernews · nazgulsenpai · Nov 12, 18:17

**「Background」** Microsoft 365 is delivered as a hosted cloud service, so failures in Microsoft&\#x27;s infrastructure can block access to its services even when users&\#x27; local systems are working. Microsoft uses a service status page to post incident details; users in this discussion reported that the page would not load reliably and instead followed its RSS feed for updates.

**「Impact」** Affected organizations lost access to Microsoft 365 services, and one commenter said much of their organization was halted. Because the public status page was not loading reliably, at least one user relied on Microsoft&\#x27;s RSS feed to receive incident updates.

**「Community discussion」** Commenters shared operational experiences and broader explanations: one linked the outage to Microsoft&\#x27;s reported workforce reductions and said much of their organization was halted, while another argued that software and service quality has been declining for several years. A third commenter said they were surprised that GitHub and GitHub Actions were still working while many other services were reported down.

**Tags**: `#Microsoft 365`, `#Azure`, `#cloud outage`, `#service reliability`, `#incident response`

---

<a id="item-tech-news-10"></a>
### [Why Writing Correct Software Is Hard: Formal-Methods Debate](https://pron.github.io/posts/correctness-and-complexity) ⭐️ 7.0/10

This item is an evergreen essay rather than a release or incident: Ari Fordsham&\#x27;s &quot;Why Writing Correct Software Is Hard&quot; examines why establishing software correctness is difficult and drew a Hacker News discussion about formal methods and real-world constraints. Commenters debated whether &quot;correct&quot; is well-defined and whether formal specification pays off outside a small core, such as database logic, rather than across peripheral scripts and CLIs. The thread also included a technical objection that the essay conflates Rice&\#x27;s Theorem with a claim about a specific small program.

hackernews · AriFordsham · Nov 12, 10:28 · [Discussion](https://news.ycombinator.com/item?id=50465352)

**「Background」** The essay under discussion is Ron Pressler&\#x27;s July 23, 2016 post, which reviews results from computability and complexity theory to argue that programs and the complete understanding required for correctness are fundamentally at odds. The current Hacker News thread revisits that argument and debates formal methods, real-world constraints, and how to define correctness.

**「Community Discussion」** Commenters disagreed about whether correctness is even well-defined: turbobutton distinguished mathematical correctness from functioning in messy real-world workflows, cadamsdotcom argued that only a small subset of software—such as core database logic—benefits from formal specification, and hinkley compared software to contract law, where acceptable inputs, outputs, and intermediate states cannot all be pinned down. johnbender separately criticized the essay for conflating Rice&\#x27;s Theorem with a claim about a specific small program.

<details><summary>References</summary>
<ul>
<li><a href="https://pron.github.io/posts/correctness-and-complexity">Why Writing Correct Software Is Hard - Ron Pressler</a></li>
<li><a href="https://news.ycombinator.com/item?id=50465352">Why Writing Correct Software Is Hard | Hacker News</a></li>

</ul>
</details>

**Tags**: `#software correctness`, `#formal verification`, `#software engineering`, `#complexity`, `#HN discussion`

---

<a id="item-tech-news-11"></a>
### [Google launches Gemini Decision 1 decisions API with multimodal inputs](https://simonwillison.net/2026/Nov/11/gemini-decisions-api/) ⭐️ 7.0/10

Google has released a Gemini Decisions API built on Gemini Decision 1, a structured decision model for developers that answers yes/no, multiple-choice, and rubric-scoring questions. According to Simon Willison, it covers text, images, audio, video, and PDFs, and it is priced at $0.10 per million input tokens with output free — matching OpenAI&\#x27;s GPT-6 Luna decision model but above Jev&\#x27;s $0.042 per million. In Willison&\#x27;s video test, Gemini returned probabilities for yes/no questions \(for example, 0.9234 that a robot appeared\) rather than the strict 1.0/0.0 answers he says Jev and OpenAI return. The supplied Telegram summary says it is available in Google AI Studio and can score up to 1,000 questions per request with roughly 150–250 ms end-to-end latency, a vendor performance claim.

rss · Simon Willison · Nov 11, 22:03

**「Background」** Decision APIs are a narrower alternative to general chat completions: callers submit closed questions—yes/no, choice, or rubric-scoring—and receive structured scores or probabilities instead of prose. Before Gemini Decision 1, Jev and OpenAI&\#x27;s GPT-6 Luna model occupied this category, with Jev limited to text and JSON and OpenAI handling text and images.

**「Impact」** For teams that need to classify video, audio, or PDFs, Gemini Decision 1 is the only one of the three decision APIs cited here with those input types, but its probability outputs require callers to set their own thresholds instead of relying on boolean 1.0/0.0 results. Cost-sensitive text-only workloads still have a cheaper option in Jev at $0.042 per million input tokens; at $0.10, Gemini matches GPT-6 Luna.

**Tags**: `#Gemini API`, `#decision models`, `#multimodal AI`, `#API pricing`, `#Google AI`

---

<a id="item-tech-news-12"></a>
### [Audit finds TRIBE v2 lacks retinotopic and tonotopic maps but shows MT+ selectivity](https://www.reddit.com/r/MachineLearning/comments/1xuillf/does_metas_brainresponse_model_tribe_v2_actually/) ⭐️ 7.0/10

A self-funded, non-peer-reviewed audit posted to r/MachineLearning tested whether Meta&\#x27;s TRIBE v2 — a model that predicts fMRI responses from video, audio and text — reproduces classic topographic maps that its paper never checked. Running standard mapping stimuli \(checkerboard wedges and rings, hemifield flicker, moving dots, tone sweeps\) through the model and fitting the same analyses used on real fMRI, the author reports no retinotopic map \(d=0.05, not significant\) and no tonotopic map \(ρ=-0.07, not significant, even with loudness controlled\), but strong motion selectivity localized to MT+ \(d=4.31, 52x enrichment over chance\). The author also notes that TRIBE v2&\#x27;s methods section states video features are spatially averaged before prediction, which should degrade position information, and that an eccentricity effect appeared only after three stimulus-geometry controls were applied — read as an image-statistics confound rather than a positional code. The work is a solo, unverified audit with a synthetic ground-truth control, not a peer-reviewed replication.

reddit · r/MachineLearning · /u/Own\_Tank1283 · Nov 12, 17:16

**「Background」** Meta announced TRIBE v2 in March 2026 as a deep multimodal encoding model that predicts fMRI responses to naturalistic video, audio, and text, mapping pretrained embeddings onto the cortical surface; Meta says it builds on its Algonauts 2025 model and was trained on data from more than 700 healthy volunteers. The audit applies classic fMRI mapping paradigms—retinotopic wedge/ring stimuli, tonotopic sweeps, and moving-dot localizers—which test whether a model recovers position- and motion-selective organization rather than only predicting responses to naturalistic stimuli.

**「Impact」** For researchers using TRIBE v2 as a brain-encoding benchmark, the audit argues that strong prediction accuracy does not by itself demonstrate topographic organization: motion selectivity replicates cleanly, but position and frequency maps do not. The eccentricity result in particular suggests that any apparent spatial code should be tested against stimulus-geometry and image-statistics controls before being interpreted as recovered retinotopy.

<details><summary>References</summary>
<ul>
<li><a href="https://aidemos.atmeta.com/tribev2/">TRIBE v2 - aidemos.atmeta.com</a></li>
<li><a href="https://github.com/facebookresearch/tribev2">GitHub - facebookresearch/tribev2: This repository contains ...</a></li>
<li><a href="https://ai.meta.com/blog/tribe-v2-brain-predictive-foundation-model/">Introducing TRIBE v2: A Predictive Foundation Model Trained ...</a></li>

</ul>
</details>

**Tags**: `#fMRI`, `#TRIBE v2`, `#model evaluation`, `#computational neuroscience`, `#reproducibility`

---

## Technology Blog

<a id="item-tech-blog-1"></a>
### [vLLM-Omni Brings MiniMax H3-Image to Vera Rubin](https://vllm.ai/blog/2026-11-12-minimax-h3-image-rubin) ⭐️ 7.0/10

rss · vLLM Blog · Nov 12, 00:00

**「Background」** MiniMax&\#x27;s open-weight H3-Image handles both text-to-image generation and editing from one checkpoint, producing native high-resolution output in six sampling steps without an upscaler, and it accepts up to 16 reference images. Serving it at 4K is demanding: each 4096×4096 result contributes 16,384 target-image tokens across those denoising steps before VAE decoding, so the vLLM-Omni team set out to measure how far Rubin&\#x27;s capabilities could be turned into interactive latency and throughput.

**「Solution」** The team connected Omni&\#x27;s diffusion linears to vLLM&\#x27;s online MXFP8 loading and kernel selection, so eligible DiT linears on Rubin use FlashInfer CuTe-DSL MXFP8 GEMMs while the text encoder and VAE keep native precision, and Ulysses SP4 spreads sequence work across four GPUs with DiT weights replicated. Repeated 4K requests exposed a stall in output transfer, which they fixed by moving final image-layout conversion to the CPU after transferring the decoded uint8 tensor. VAE tiles are distributed across GPUs and, on each GPU, CUDA Graph replay is combined with multiple streams; in a BF16 control this cut VAE decoding from 2.635 s to 0.213 s and end-to-end latency from about 4.0 s to 1.6 s. With SP4 at concurrency 1, median latency was 0.866 s \(p95 0.944 s\), 2.21× faster than GB200 and 1.64× faster than GB300, while four single-GPU replicas reached 6,115 images/hour versus SP4&\#x27;s 4,407. The authors caution that the 0.87 s headline comes from a short-prompt benchmark \(20 prompts, eight seeds\), whereas a 1,292-character coffee prompt averages 1.09 s, and that results compare deployed systems rather than isolating GPU architecture.

**「Takeaway」** The authors present H3-Image as evidence that diffusion serving on new hardware is mostly systems work—precision, parallelism, decoding overlap, and transfer-path reliability—and their revenue projections \(USD 105.16/GPU/hour at full utilization, before operating costs\) remain extrapolations from a measured rate, not a 24-hour load test.

**Tags**: `#diffusion model serving`, `#GPU inference optimization`, `#benchmarking methodology`, `#VAE decoding`, `#vLLM-Omni`

---

## Financial News

<a id="item-finance-news-1"></a>
### [礼来口服减重药在中国获批，为国内首个口服GLP-1减重药](https://www.reuters.com/business/healthcare-pharmaceuticals/china-approves-eli-lillys-weight-loss-pill-orforglipron-2026-11-12/) ⭐️ 8.0/10

礼来口服GLP-1减重药奥氟格列隆钙片（商品名穆优达）于11月12日获中国国家药监局批准为1类新药，用于肥胖或超重且伴有至少一种体重相关合并症的成人，成为国内首个获批的口服GLP-1减重药。据路透社报道，该药每日服用一次，不受饮食饮水限制，其2型糖尿病适应证仍在审评中，价格和上市时间尚未公布。

telegram · zaihuapd · Nov 12, 10:09

**「Background」** Until now, GLP-1 weight-loss drugs on the Chinese market have been given as weekly injections, the category the new pill will compete against. Orforglipron itself is a once-daily pill taken without food or water restrictions and was approved in the US in April 2026, according to a competitive-landscape analysis.

**「Impact」** Adults in China with obesity or overweight plus at least one weight-related condition gain a once-daily oral alternative to weekly injectable weight-loss drugs, putting Lilly into competition with Novo Nordisk, Pfizer and Innovent in the country’s weight-loss market.

<details><summary>References</summary>
<ul>
<li><a href="https://eureka.patsnap.com/blog/life-science/esc-2026-glp-1-receptor-agonists-competitive-landscape-analysis/">GLP - 1 Receptor Agonists Competitive Landscape Analysis 2026</a></li>

</ul>
</details>

**Tags**: `#礼来`, `#口服GLP-1`, `#减重药`, `#中国药监局批准`, `#医药行业`

---

<a id="item-finance-news-2"></a>
### [Fed to Skip Rate Vote at October 2027 Meeting](https://www.cnbc.com/2026/11/12/in-policy-switch-fed-says-its-october-2027-meeting-will-not-see-a-vote-on-interest-rates.html) ⭐️ 7.0/10

The Federal Reserve will hold seven voting meetings in 2027, with its Oct. 26-27 session set aside for broad monetary-policy strategy discussions rather than an interest-rate vote or post-meeting statement. The final meeting of the year moves to November from December as part of Chairman Kevin Warsh&\#x27;s communication overhaul.

rss · CNBC Finance · Nov 12, 19:05

**「Background」** The Fed typically holds eight policy meetings a year and votes on rates at each, a convention Kiplinger dates to 1981; Chair Kevin Warsh has already shortened post-meeting statements and press conferences as part of a communication overhaul.

<details><summary>References</summary>
<ul>
<li><a href="https://www.kiplinger.com/news/live/fed-meeting-updates-and-commentary-june-2026">June Fed Meeting : Updates and Commentary | Kiplinger</a></li>

</ul>
</details>

**Tags**: `#Federal Reserve`, `#monetary policy`, `#FOMC`, `#Kevin Warsh`, `#central bank communication`

---