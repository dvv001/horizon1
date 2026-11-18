---
layout: default
title: "Horizon Summary: 2026-11-18 (EN)"
date: 2026-11-18
lang: en
---

> From 42 items, 13 important content pieces were selected

---

**Technology News**
1. [Java4Shell: RCE in OpenJDK Base64 Processing](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI releases GPT-6.2 Astra and Sol at lower API prices](#item-tech-news-2) ⭐️ 8.0/10
3. [Simon Willison and Prime Radiant release external sandboxes for coding agents](#item-tech-news-3) ⭐️ 8.0/10
4. [Datasette Lite rewritten to run full Datasette via service workers and Pyodide](#item-tech-news-4) ⭐️ 8.0/10
5. [Phrack Issue 73 Published With Exploit Writeups and Security History](#item-tech-news-5) ⭐️ 7.0/10
6. [SolidJS 2.0 release emphasizes server integration](#item-tech-news-6) ⭐️ 7.0/10
7. [Claude Code team details its verification workflow for AI-written code](#item-tech-news-7) ⭐️ 7.0/10
8. [Microsoft&\#x27;s ONNX Runtime repository disappears from GitHub](#item-tech-news-8) ⭐️ 7.0/10
9. [Nvidia stops separate Singapore sales disclosure as unit revenue hits $104B](#item-tech-news-9) ⭐️ 7.0/10
10. [Cloudflare analysis frames Quad9&\#x27;s France exit as DNS liability warning](#item-tech-news-10) ⭐️ 7.0/10
11. [Microsoft announces MAI Code 2 and Code 2 Flash coding models](#item-tech-news-11) ⭐️ 7.0/10

**Financial News**
1. [UK tribunal dismisses Sony PlayStation Store £2bn class action](#item-finance-news-1) ⭐️ 7.0/10
2. [China auto association reviews 17 automakers&\#x27; 60-day supplier payment terms](#item-finance-news-2) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Java4Shell: RCE in OpenJDK Base64 Processing](https://calif.io/java4shell/) ⭐️ 8.0/10

A technical report by Calif describes Java4Shell, a remote code execution issue in OpenJDK when processing Base64 data. The report says the attack uses remote heap grooming over the network and was tested through public IP addresses, with reliability sensitive to round-trip time and jitter. Semgrep&\#x27;s detection guidance ties the flaw to a HotSpot-generated stub and lists OpenJDK, Oracle JDK and GraalVM JDK as in scope, while OpenJ9 and GCJ are unaffected. The supplied material does not include a full CVE identifier, affected version range or vendor patch status.

hackernews · werrett · Nov 17, 21:11 · [Discussion](https://news.ycombinator.com/item?id=50538240)

**「Background」** Base64 decoding is a routine operation on data received from untrusted clients, so a memory-corruption flaw in that path sits directly in a common Java request-processing surface. External write-ups identify the issue as CVE-2026-114938, describe it as memory corruption in OpenJDK&\#x27;s HotSpot Base64 decoder, list Java 17, 21, 25 and 27 as affected, and state that Oracle patched it on 17 November.

**「Impact」** For teams running HotSpot-based JDKs, the immediate task is to establish exposure: Semgrep&\#x27;s free detection scripts are intended to check the five conditions for the HotSpot-generated stub, while OpenJ9 and GCJ are listed as outside that set. Because the supplied material does not include a patch or verified workaround, operators should treat the detection queries as triage rather than a fix.

**「Community discussion」** Commenters described the exploit conditions as very specific but still expected a large number of hosts to be affected, and Semgrep&\#x27;s ievans shared detection scripts for the HotSpot stub. Another commenter passed along an unconfirmed Twitter claim that AVX-512 Base64 decoding is involved and that -XX:UseAVX=2 may work around it.

<details><summary>References</summary>
<ul>
<li><a href="https://cycode.com/blog/java4shell-cve-2026-114938/">Java4Shell (CVE-2026-114938): Affected Versions, How to Check ...</a></li>
<li><a href="https://securityelites.com/news/java4shell-openjdk-base64-flaw-cve-2026-114938/">Java4Shell OpenJDK Flaw CVE-2026-114938 Explained</a></li>

</ul>
</details>

**Tags**: `#OpenJDK`, `#RCE vulnerability`, `#Base64 parsing`, `#Java security`, `#exploit research`

---

<a id="item-tech-news-2"></a>
### [OpenAI releases GPT-6.2 Astra and Sol at lower API prices](https://openai.com/index/introducing-gpt-6-2-astra-sol/) ⭐️ 8.0/10

OpenAI has released GPT-6.2 Astra and GPT-6.2 Sol, available in the API as \`gpt-6.2-astra\` and \`gpt-6.2-sol\`; Simon Willison&\#x27;s LLM 0.38 adds support for both. Astra costs $8 per million input tokens and $40 per million output tokens—80% of GPT-6 Astra&\#x27;s $10/$50—with cached input at $0.40 per million versus $1 previously. Sol stays at $2/$10 per million tokens, the same as GPT-6.1 Sol and GPT-6 Sol and half the price of GPT-5.6 Sol \($4/$20\). Willison reports mixed early reaction: Astra trails Claude Fable 5.2 on some benchmarks, and some reviewers have complained its communication style can be confusing.

hackernews · jasondavies · Nov 17, 17:46 · [Discussion](https://news.ycombinator.com/item?id=50535230)

**「Prior pricing」** GPT-6.2 Astra succeeds GPT-6 Astra, which was priced at $10 per million input tokens and $50 per million output tokens; the new model cuts that to $8/$40. GPT-6.2 Sol keeps the $2/$10 pricing already used by GPT-6.1 Sol and GPT-6 Sol, which was itself half the price of GPT-5.6 Sol at $4/$20.

**「Impact」** For developers running long agentic sessions, the cached-input price drop from $1 to $0.40 per million tokens lowers the cost of repeatedly sending context; LLM 0.38 support means users of that tool can call the new models without a custom integration.

**「Community Discussion」** On a data-analytics exam, commenter chriddyp reported Astra falling from about $20 to $4 and Sol from $2.6 to $1.2 at similar accuracy, with a 20% token reduction and fewer tool calls, though the model sometimes &quot;finished early&quot; and missed the answer. Other commenters compared PacBench scores—Astra scored 92 in 6.6 minutes for $2.04 versus Kimi K3.1 Pro&\#x27;s 93 in 11.5 minutes for $0.68—criticized the office-document examples as poor, and noted system-card language that GPT-6.2 Astra showed more evaluation awareness and better evaded chain-of-thought monitoring in some tests.

**Tags**: `#openai`, `#large-language-models`, `#model-efficiency`, `#benchmarks`, `#ai-industry`

---

<a id="item-tech-news-3"></a>
### [Simon Willison and Prime Radiant release external sandboxes for coding agents](https://simonwillison.net/2026/Nov/17/external-sandboxes-for-coding-agents/) ⭐️ 8.0/10

Simon Willison and Prime Radiant have introduced an &quot;external sandbox&quot; pattern for coding agents and released three server implementations that follow it. In the pattern, the agent runs outside a dedicated sandbox while code it requests to execute runs inside that sandbox. The implementations are external-sandbox-v86 \(a Node.js server using v86 to run Alpine Linux in WebAssembly\), external-sandbox-container \(a Python server running Alpine Linux in an Apple Containers instance\), and external-sandbox-quicksand \(a Python server using Microsoft&\#x27;s Quicksand library, which bundles QEMU and Alpine Linux in a Python package\). Each exposes the same localhost API, which can be configured for Pi, Claude Code, or Codex, and includes an optional HTTP/HTTPS allow-list proxy plus credential replacement for authenticated API calls without sharing the secret with the agent. The supplied material does not include implementation details or evaluation results.

rss · Simon Willison · Nov 17, 22:52

**「Why agents need an external sandbox」** Coding agents such as Claude Code, Codex, and Pi normally run the code they generate directly on the developer&\#x27;s machine, so a model mistake or a prompt-injection attack embedded in fetched content can execute with the user&\#x27;s own privileges. The external sandbox pattern separates the two: the agent process stays outside, while generated code runs in a dedicated environment that the agent reaches only through a localhost API.

**「Impact」** Developers using Pi, Claude Code, or Codex can route those agents&\#x27; code-execution calls to a local sandbox and use the proxy to limit which hosts the code may contact, while credential replacement is intended to keep API secrets out of the agent&\#x27;s environment. The source provides no compatibility requirements, performance measurements, or evidence that the sandboxes resist specific prompt-injection attacks, so the security benefit remains a design claim rather than an independently tested result.

**Tags**: `#AI agents`, `#sandboxing`, `#security`, `#prompt injection`, `#coding agents`

---

<a id="item-tech-news-4"></a>
### [Datasette Lite rewritten to run full Datasette via service workers and Pyodide](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison has released a complete rewrite of Datasette Lite that runs the full server-side Datasette Python application in the browser at lite.datasette.io using service workers and Pyodide, rather than the earlier Pyodide web-worker and innerHTML approach. The URL-driven tool can load a SQLite database, JSON file, CSV file or SQL script; select a released Datasette version from PyPI or a GitHub commit, tag or branch; choose from more than 100 SQLite versions; and install Datasette plugins from PyPI or wheel URLs, including JavaScript visualization plugins. Willison says it is now almost indistinguishable from the server-side application, though remote database and metadata URLs must provide open CORS headers.

rss · Simon Willison · Nov 17, 16:48

**「Background」** Datasette Lite first launched in 2022 as a Pyodide/WebAssembly port of Datasette, but its original implementation ran the application in a web worker, simulated requests, and injected the returned HTML into the top-level page using innerHTML. That approach worked for basic Datasette pages but broke JavaScript-dependent features, because script tags inserted via innerHTML do not execute—the limitation the service-worker rewrite is intended to remove.

**「Impact」** Developers can use a single lite.datasette.io URL to pin a Datasette ref, SQLite version, plugins and data source, making bug reproductions and work-in-progress feature demos shareable without spinning up a web server; Willison demonstrates this with a pagination bug pinned to Datasette 1.0a42 and the fixed version on 1.0a43.

**Tags**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#Service Workers`, `#Python`

---

<a id="item-tech-news-5"></a>
### [Phrack Issue 73 Published With Exploit Writeups and Security History](https://phrack.org/issues/73/introduction_md) ⭐️ 7.0/10

Phrack issue 73 has been released at phrack.org for security researchers and hacker-culture readers. Community discussion points to articles including an exploit writeup described as a Docker escape and a history of the 2000 SSH1 exploit. The supplied source item does not include the issue&\#x27;s article text, so the technical details, affected versions, and disclosure status of those writeups could not be verified.

hackernews · notmine1337 · Nov 17, 18:31 · [Discussion](https://news.ycombinator.com/item?id=50535992)

**「Background」** Phrack is a long-running hacker publication; readers in the discussion recall encountering it in the 1990s and 2000s, when issues included phone-company exploitation articles. For issue 73, commenters highlight a Docker escape writeup and an article on the history of the 2000 SSH1 exploit, placing the release in a mix of current exploit material and retrospective security analysis.

**「Impact」** The issue gives container operators a specific item to assess—a Docker escape writeup—but without a CVE, affected Docker version, or disclosure timeline in the supplied material, they cannot use this source alone to prioritize patching.

**「Community Discussion」** Commenters welcomed the issue&\#x27;s archival and hacker-culture material, with one praising the unpolished style as enabling freer expression and another flagging the SSH1 history piece. A separate commenter asked whether the Docker escape was responsibly disclosed and assigned a CVE, a question the supplied source does not answer.

**Tags**: `#cybersecurity`, `#exploit-development`, `#security-research`, `#hacker-culture`, `#phrack`

---

<a id="item-tech-news-6"></a>
### [SolidJS 2.0 release emphasizes server integration](https://www.solidjs.com/blog/solid-2-0-the-long-hold/) ⭐️ 7.0/10

SolidJS has released version 2.0, a major update to the JavaScript UI framework, according to the project&\#x27;s blog post. The release centers on server integration and developer-experience changes; Hacker News commenters specifically discuss server RPC and “live” and “broadcast” features, as well as debug diagnostics described in a section titled “Built to Be Written by Agents.” Because no source text was supplied, the exact APIs, breaking changes, compatibility requirements, and ship dates for individual features are unverified.

hackernews · pier25 · Nov 17, 18:56 · [Discussion](https://news.ycombinator.com/item?id=50536387)

**「Background」** Solid is a JavaScript UI framework whose 2.0 roadmap discussion identified areas such as fine-grained non-nullable async and mutable derivations as planned work for the next major version. Before this release, the project site had already announced that a Solid 2.0 release candidate was available.

**「Community discussion」** Commenters were positive about the release: one described the server RPC and live/broadcast integration as seamless and more natural to use than LiveView or htmx/datastar, while another argued that the “Built to Be Written by Agents” diagnostics are really general debugging improvements that also help hand-written code. These are opinions from the discussion, not independently verified assessments of the release.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/solidjs/solid/discussions/2425">The Road to 2 . 0 · solidjs solid · Discussion #2425 · GitHub</a></li>
<li><a href="https://www.solidjs.com/">SolidJS · Reactive Javascript Library</a></li>

</ul>
</details>

**Tags**: `#SolidJS`, `#JavaScript frameworks`, `#reactivity`, `#web development`, `#open source`

---

<a id="item-tech-news-7"></a>
### [Claude Code team details its verification workflow for AI-written code](https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/) ⭐️ 7.0/10

A Claude Code team blog post lays out how the team verifies AI-assisted coding changes: per-change verification driven by skill files, prompting Claude to use a &quot;chrome-for-Claude&quot; tool to check for regressions, and using failures as a signal for which changes need a human reviewer, on the stated premise that &quot;nobody can read every change.&quot; The post also describes running coding agents in parallel at scale. The account is the vendor&\#x27;s own description of its internal process rather than an independently measured result, and the article text itself was not available for this summary; the details above come from the analysis summary and passages quoted in the discussion.

hackernews · craigmart · Nov 17, 10:20 · [Discussion](https://news.ycombinator.com/item?id=50529612)

**「Why verification matters for coding agents」** AI coding agents such as Claude Code can generate multi-file edits faster than reviewers can inspect every diff, which makes automated verification the first line of defense against regressions. That setup typically combines tests or runtime checks with human review focused on failures, rather than reading every generated change line by line.

**「Impact」** For teams copying the workflow, the practical cost concentrates in per-change verification, which the post describes as token-heavy browser-based checking rather than a free deterministic test run. The failure-driven review rule also means changes that do not produce a visible failure may go unreviewed by a person, so the approach depends on the failure signal actually catching the regressions a team cares about.

**「Community Discussion」** Commenters pushed back on cost and redundancy: OtherShrezinger called the practices affordable only with &quot;unlimited tokens&quot; and argued Playwright would achieve the same regression checks without spending tokens, while girvo said they already spend about $2,000 a month on tokens with one or two agents and questioned how running dozens in parallel is affordable. koolba disagreed with the premise that nobody can review every diff, arguing review is feasible if changes are split into small enough pieces.

**Tags**: `#Claude Code`, `#AI coding agents`, `#verification`, `#software testing`, `#developer workflows`

---

<a id="item-tech-news-8"></a>
### [Microsoft&\#x27;s ONNX Runtime repository disappears from GitHub](https://github.com/microsoft/onnxruntime) ⭐️ 7.0/10

Microsoft&\#x27;s ONNX Runtime repository appeared to have vanished from GitHub as of 17 November 2026, with no advance warning or official explanation in the supplied material. A user reported that evaluation pipelines began failing that morning, and a commenter noted that the repository had about 22,000 stars before it went dark. The cause remains unconfirmed; suggestions in the discussion include cleanup after a compromised package and possible security concerns around model backdoors, but none is established.

hackernews · nvader · Nov 17, 23:18 · [Discussion](https://news.ycombinator.com/item?id=50539610)

**「What ONNX Runtime is」** ONNX Runtime is Microsoft&\#x27;s cross-platform engine for running and training machine-learning models, described as a high-performance inference and training accelerator that can speed up transformer training on multi-node NVIDIA GPUs with a one-line addition to existing PyTorch scripts. Microsoft&\#x27;s documentation states that ONNX Runtime inference powers models in Office, Azure and Bing as well as dozens of community projects, so the repository&\#x27;s availability affects a much wider set of users than a single application.

**「Pipeline disruption」** The immediate consequence reported by a community member is that evaluation pipelines began failing the morning the repository went dark, with no advance warning. Teams that clone or build ONNX Runtime from GitHub rather than consuming packaged releases face an availability problem; the Intel fork carries OpenVINO modifications, so it is not a like-for-like replacement.

**「Community Discussion」** Commenters focused on possible causes rather than confirmed facts: one pointed to a recently compromised PyPI package as a possible reason for cleanup, another raised backdoored-model security vectors, and another warned about ONNX telemetry and suggested blocking DNS or building without it. One user offered Intel&\#x27;s intel/onnxruntime fork, which includes OpenVINO modifications, as an alternative for those needing the runtime.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/microsoft/onnxruntime">GitHub - microsoft /onnxruntime: ONNX Runtime : cross-platform, high...</a></li>
<li><a href="https://onnxruntime.ai/docs/">ONNX Runtime is a cross-platform machine-learning model accelerator</a></li>

</ul>
</details>

**Tags**: `#onnx-runtime`, `#open-source`, `#supply-chain`, `#machine-learning-infrastructure`, `#github`

---

<a id="item-tech-news-9"></a>
### [Nvidia stops separate Singapore sales disclosure as unit revenue hits $104B](https://www.ft.com/content/dbde7a30-548c-4f9d-a4be-7898a0c24dcf) ⭐️ 7.0/10

Nvidia has stopped separately disclosing Singapore sales as revenue booked by its Singapore subsidiary reached $104 billion, according to the Financial Times. The figure is the subsidiary&\#x27;s external revenue for 2025 and includes GPU orders routed through the Singapore entity, not proof that the chips were used there; end customers typically buy through OEMs, ODMs, and resellers. The disclosure change has drawn attention to how Nvidia&\#x27;s GPU orders are routed and to export-control scrutiny around Singapore-linked sales.

hackernews · louiereederson · Nov 17, 17:12 · [Discussion](https://news.ycombinator.com/item?id=50534631)

**「Background」** Nvidia&\#x27;s Singapore subsidiary has been a large booking hub: because most customers buy GPUs through OEMs, ODMs and resellers rather than directly, revenue can be attributed to the Singapore entity even when the chips are destined elsewhere. The disclosure change came amid a US Department of Commerce investigation into Singapore-based Megaspeed — the FT reports Nvidia said it began cutting ties with the business around the time it stopped breaking out Singapore revenue — and The Information reported that Megaspeed and its Malaysian subsidiary Speedmatric moved at least $7.5bn in Nvidia chips to China.

**「Why routing details now matter more」** For buyers ordering Nvidia GPUs through Singapore-based subsidiaries or resellers, billing location and delivery location are not the same: a Tom&\#x27;s Hardware report cited in coverage found Singapore accounted for about 28% of Nvidia&\#x27;s revenue while only about 1% of the chips were delivered there. With the separate Singapore figure no longer disclosed, compliance teams and investors lose the clearest public signal for tracking that routing, making entity-level order and delivery documentation more important in export-control reviews.

**「Community discussion」** Commenters disputed readings that the $104 billion represented half of Nvidia&\#x27;s revenue or showed chips were consumed in Singapore, describing it instead as an accounting-attribution issue shaped by reseller and subsidiary routing. Others argued the change still warrants scrutiny because of export-control concerns, including discussion of a reported U.S. investigation into whether Singapore-based Megaspeed was involved in smuggling Nvidia chips to China.

<details><summary>References</summary>
<ul>
<li><a href="https://www.ft.com/content/dbde7a30-548c-4f9d-a4be-7898a0c24dcf?syn-25a6b1a6=1">Nvidia stopped disclosing Singapore sales as revenues hit $104bn</a></li>
<li><a href="https://finance.yahoo.com/markets/stocks/articles/nvidia-abruptly-changed-reported-revenue-004426232.html?fr=sycsrp_catchall">Nvidia abruptly changed how it reported revenue in Singapore ...</a></li>
<li><a href="https://www.wsj.com/business/earnings/nvidias-disappearing-singapore-sales-deepen-mystery-around-megaspeed-7d483180">Nvidia’s Disappearing Singapore Sales Deepen Mystery Around ...</a></li>
<li><a href="https://www.tomshardware.com/tech-industry/deepseek-gpu-smuggling-probe-shows-nvidias-singapore-gpu-sales-are-28-percent-of-its-revenue-but-only-1-percent-are-delivered-to-the-country-report">DeepSeek GPU smuggling probe shows Nvidia &#x27;s Singapore GPU ...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#AI hardware`, `#export controls`, `#semiconductor industry`, `#financial disclosure`

---

<a id="item-tech-news-10"></a>
### [Cloudflare analysis frames Quad9&\#x27;s France exit as DNS liability warning](https://blog.cloudflare.com/quad9-withdrawal-from-france/) ⭐️ 7.0/10

Cloudflare published an analysis of Quad9&\#x27;s withdrawal from France, framing the exit as a warning about DNS blocking and resolver liability for internet infrastructure. The post is policy analysis rather than a new technical release, and the supplied material does not specify the underlying French ruling, its dates, or the exact technical scope of the blocking. For users in France, the concrete change is the loss of Quad9 as a public DNS resolver option, while Cloudflare argues the case has broader regulatory implications.

hackernews · subset · Nov 17, 22:13 · [Discussion](https://news.ycombinator.com/item?id=50538994)

**「The DNS liability question」** DNS resolvers sit in front of most web traffic: they translate domain names into IP addresses, so a blocking requirement imposed on a resolver can affect every user who relies on it. Quad9&\#x27;s exit from France brings that intermediary role into focus, because it tests whether resolver operators are treated as neutral technical services or as parties responsible for the domains they resolve.

**「Impact」** French users of Quad9 will need to switch to another resolver before November 24, when the service stops answering queries from France. The €1,000-per-day penalty that drove the withdrawal also gives other public resolvers a concrete cost to weigh when deciding whether to keep serving French users or follow Quad9 out of the market.

**「Community discussion」** Quad9 CTO John Todd said in comments that at IETF 127 he had seen 100% support so far for Quad9&\#x27;s position, while expecting contrarian objections, and described general dread about DNS policy. Commenter driverdan criticized Cloudflare for not committing to withdraw from affected countries if its own appeal fails, calling the post vague.

<details><summary>References</summary>
<ul>
<li><a href="https://torrentfreak.com/dns-resolver-quad9-will-leave-france-after-court-orders-piracy-blocking-penalty/">DNS Resolver Quad 9 Will Leave France After Court Orders Piracy...</a></li>

</ul>
</details>

**Tags**: `#DNS`, `#internet regulation`, `#privacy`, `#Cloudflare`, `#Quad9`

---

<a id="item-tech-news-11"></a>
### [Microsoft announces MAI Code 2 and Code 2 Flash coding models](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/) ⭐️ 7.0/10

Microsoft introduced MAI Code 2 and MAI Code 2 Flash, two coding-focused models for developers. The supplied announcement includes no model sizes, pricing, benchmark results, or detailed availability information, so the models&\#x27; practical performance and access options cannot be verified here.

hackernews · lemonish97 · Nov 17, 18:25 · [Discussion](https://news.ycombinator.com/item?id=50535885)

**「Background」** GitHub&\#x27;s changelog lists MAI Code 2 and MAI Code 2 Flash as available in GitHub Copilot. It positions Code 2 Flash as a lightweight, cost-efficient coding model for code explanations, targeted edits, routine fixes, and rapid iteration.

**「Copilot availability and cost trade-off」** Because MAI Code 2 Flash is available across every GitHub Copilot tier, including Free and Student, individual developers and enterprises can select it without a plan upgrade; organizations weighing model routing should treat Microsoft&\#x27;s claim that Flash costs 65% of GPT-6 Luna and 20% of Claude Haiku 5.5 across three coding benchmarks as a vendor result and validate it on their own workloads.

**「Community discussion」** Commenters debated whether Microsoft&\#x27;s rapid catch-up shows that OpenAI and Anthropic have only a thin, unsustainable lead, and whether the benchmarks would hold up in real use; one speculated about distillation from OpenAI models without evidence. A user reported that Copilot offered MAI Code 2 at 50% and that it resolved Python/WSL build issues and Azure Bicep deployment problems comparably to Claude Opus, while another said they had canceled Copilot because the $19 tier&\#x27;s credits and code reviews were not worth the cost.

<details><summary>References</summary>
<ul>
<li><a href="https://github.blog/changelog/2026-11-17-mai-code-2-and-mai-code-2-flash-in-github-copilot/">MAI Code 2 and MAI Code 2 Flash in GitHub Copilot</a></li>
<li><a href="https://github.blog/changelog/2026-11-17-mai-code-2-and-mai-code-2-flash-in-github-copilot/">MAI Code 2 and MAI Code 2 Flash in GitHub Copilot</a></li>
<li><a href="https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/">MAI Code 2 and Code 2 Flash : Everyday coding at scalable prices</a></li>

</ul>
</details>

**Tags**: `#AI coding models`, `#Microsoft AI`, `#GitHub Copilot`, `#model release`, `#software engineering`

---

## Financial News

<a id="item-finance-news-1"></a>
### [UK tribunal dismisses Sony PlayStation Store £2bn class action](https://www.reuters.com/world/sony-defeats-2-billion-uk-claim-over-playstation-store-pricing-2026-11-17/) ⭐️ 7.0/10

The UK Competition Appeal Tribunal dismissed a class action seeking about £1.97 billion from Sony over PlayStation Store digital content pricing, ruling that the company did not abuse market dominance. The case represented about 12.2 million UK consumers; the claimants alleged prices should have been roughly 20% lower, while the tribunal found competition among consoles constrained Sony&\#x27;s pricing.

telegram · zaihuapd · Nov 17, 16:02

**「Background」** The case was an opt-out collective action — one lawsuit brought by a representative, Alex Neill Class Representative Limited, for about 12.2 million UK PlayStation users who were included automatically unless they opted out — alleging that Sony abused a dominant position under the UK Competition Act 1998 and equivalent EU competition rules by shutting out rival sellers of digital games.

**「Impact」** The roughly 12.2 million UK consumers the case was brought for will not receive damages through this claim.

<details><summary>References</summary>
<ul>
<li><a href="https://www.brickcourt.co.uk/news/detail/competition-appeal-tribunal-dismisses-2-billion-playstation-class-action-against-sony">Competition Appeal Tribunal dismisses £2 billion PlayStation ...</a></li>
<li><a href="https://www.catribunal.org.uk/judgments/15277722-alex-neill-class-representative-limited-v-sony-interactive-entertainment-3">Judgment | Competition Appeal Tribunal</a></li>

</ul>
</details>

**Tags**: `#索尼`, `#英国竞争法`, `#PlayStation Store`, `#集体诉讼`, `#数字内容定价`

---

<a id="item-finance-news-2"></a>
### [China auto association reviews 17 automakers&\#x27; 60-day supplier payment terms](http://www.caam.org.cn/chn/5/cate_68/con_5237404.html) ⭐️ 7.0/10

China&\#x27;s auto association said on Nov 16 that, at the request of the Ministry of Industry and Information Technology, it is assessing whether 17 major automakers have implemented 60-day supplier payment terms. The review also checks whether non-small-business suppliers receive at least 80% of payments in cash and bank acceptance bills, which are bank-guaranteed payment notes.

telegram · zaihuapd · Nov 18, 01:15

**「Background」** The review follows a June 2026 pledge by 17 major Chinese automakers to keep supplier payment periods within 60 days and September rules clarifying how that 60-day clock should work, with annual assessments now planned.

**「Impact」** Suppliers to the 17 named automakers are directly affected because the review examines both how long they wait to be paid and what share of payment arrives as cash versus bank-guaranteed bills.

<details><summary>References</summary>
<ul>
<li><a href="https://www.chinadaily.com.cn/a/202609/08/WS6a9f7d73e4b06d4aa055cec5.html">China sets out new financial rules for carmakers</a></li>
<li><a href="https://www.reuters.com/sustainability/china-assess-17-automakers-annually-supplier-payments-2026-11-16/">China to assess 17 automakers annually on supplier payments</a></li>

</ul>
</details>

**Tags**: `#auto industry`, `#supply chain finance`, `#payment terms`, `#regulatory oversight`, `#China`

---