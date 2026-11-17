---
layout: default
title: "Horizon Summary: 2026-11-17 (EN)"
date: 2026-11-17
lang: en
---

> From 48 items, 15 important content pieces were selected

---

**Technology News**
1. [vLLM v0.34.0 defaults extensible KV cache, removes Model Runner V1](#item-tech-news-1) ⭐️ 8.0/10
2. [Jiff 1.0 arrives as a new Rust datetime library](#item-tech-news-2) ⭐️ 8.0/10
3. [Optimizely reportedly compromised, served malware via customer sites including Zoom and GitLab](#item-tech-news-3) ⭐️ 8.0/10
4. [US extends AI chip export controls to remote access](#item-tech-news-4) ⭐️ 8.0/10
5. [Carnegie Mellon Launches CS Learn With Free Full-Semester Lectures on YouTube](#item-tech-news-5) ⭐️ 7.0/10
6. [Windows 11 Reportedly Tracks Coding Agents and Developer Tools via Telemetry](#item-tech-news-6) ⭐️ 7.0/10
7. [Linebender wiki page covers squircle geometry for graphics](#item-tech-news-7) ⭐️ 7.0/10
8. [Microsoft blames major email outage on July fix defect](#item-tech-news-8) ⭐️ 7.0/10
9. [Marimba uses one frozen Qwen3-ASR pass for typed audio queries](#item-tech-news-9) ⭐️ 7.0/10
10. [Duetto steers a pretrained music transformer into a real-time jazz partner](#item-tech-news-10) ⭐️ 7.0/10
11. [US and nine countries sign San Francisco Declaration on AI supply chains](#item-tech-news-11) ⭐️ 7.0/10
12. [Amazon: Artex AI agents stole API keys to fund LLM use](#item-tech-news-12) ⭐️ 7.0/10
13. [Alibaba, Tencent, Moonshot Reportedly Curb Cyber Capabilities; Qwen Flagship Withholds Open Weights](#item-tech-news-13) ⭐️ 7.0/10

**Financial News**
1. [CNBC: Lutnick&\#x27;s sons&\#x27; firm cut Nvidia stake amid chip-smuggling scrutiny](#item-finance-news-1) ⭐️ 7.0/10
2. [Intel and CEO Lip-Bu Tan sued by shareholders after stock plunge](#item-finance-news-2) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0 defaults extensible KV cache, removes Model Runner V1](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM v0.34.0 is released with extensible KV-cache sizing enabled by default, Model Runner V2 as the only GPU runner after Model Runner V1&\#x27;s removal, and 10 new models including Mistral Large 4 and NVIDIA Nemotron-3.5-Transcribe. The release, spanning 1,061 commits from 412 contributors, sizes the KV cache from memory free after warmup, which the project says raises cache capacity and throughput but can increase per-token decode latency \(TPOT\) by 6–18% on some H200 models at concurrency 128. It also changes upgrade prerequisites: the default \`--block-size\` moves from 16 to 64, ROCm 7.2 artifacts are dropped in favor of ROCm 10.0, and \`huggingface\_hub &gt;= 2.0.0\`, \`tokenizers &gt;= 0.23.3\`, and \`timm &gt;= 1.0.30\` are required. Release notes claim performance gains including up to 1.95× decode for Step5 NVFP4 MoE on 4×GB200 and 1.6× output throughput for GLM-5.3-Flash.

github · khluu · Nov 16, 23:22

**「Background」** vLLM is an open-source LLM inference and serving engine, and its KV cache determines how many tokens can be held in GPU memory at once, directly affecting throughput and time-to-first-token under concurrency. Before v0.34.0, extensible KV-cache sizing was opt-in, \`gpu\_memory\_utilization\` defaulted below 1.0, and the default \`--block-size\` was 16; Model Runner V1 also remained available as an alternative to V2. This release makes the new cache sizing and Model Runner V2 the only defaults, so configurations that relied on the earlier behavior now need explicit opt-out flags or code ports.

**「Impact」** Existing deployments must remove \`VLLM\_USE\_V2\_MODEL\_RUNNER=0\` or startup will fail, port V1 logits processors to \`vllm.v1.worker.gpu.sample.logits\_processor\`, and either accept the new block size or pass \`--block-size 16\` to preserve old behavior. Operators who need the previous KV-cache sizing can pass \`--gpu-memory-utilization 0.9\` or \`--no-enable-extensible-kv-cache\`, since \`gpu\_memory\_utilization\` now defaults to 1.0.

**Tags**: `#vLLM`, `#LLM inference`, `#KV cache`, `#release notes`, `#performance`

---

<a id="item-tech-news-2"></a>
### [Jiff 1.0 arrives as a new Rust datetime library](https://burntsushi.net/jiff/) ⭐️ 8.0/10

Jiff, a datetime library for Rust from developer burntsushi, has been released at version 1.0. It is a new option for Rust programs that need date and time handling, and Hacker News discussion focused on its API design, ecosystem adoption, and treatment of time scales. The supplied material does not detail Jiff&\#x27;s API surface, compatibility guarantees, or a migration path from chrono.

hackernews · burntsushi · Nov 16, 16:53 · [Discussion](https://news.ycombinator.com/item?id=50519744)

**「Background」** Jiff is Andrew Gallant&\#x27;s Rust datetime library, and its 1.0 announcement is written as an API tour for Rust programmers who need convenient datetime handling. The tour defines TAI as International Atomic Time, an atomic-clock time standard, reflecting the fact that datetime code often has to distinguish time scales rather than only civil clock time. In the Hacker News thread, a commenter working on long-range orbital simulations asked how Jiff handles TAI and whether other scales such as UT1 could be added.

**「Impact」** Rust developers evaluating datetime crates now have a 1.0 release to consider alongside chrono; because no drop-in compatibility or migration path is described, teams should treat adoption as a code-level evaluation rather than a routine version bump.

**「Community Discussion」** A former chrono maintainer said they took on that project hoping to improve its API but found users preferred stability and resisted changes, leading to burnout; they welcomed burntsushi&\#x27;s work. Another commenter praised Jiff&\#x27;s explicit statement that it is not always the right tool, while a user simulating long-timescale orbits asked how Jiff handles time scales such as TAI and UT1.

<details><summary>References</summary>
<ul>
<li><a href="https://news.ycombinator.com/item?id=50519744">Jiff 1 . 0 : A datetime library for Rust | Hacker News</a></li>
<li><a href="https://burntsushi.net/jiff/">A datetime library for Rust - Andrew Gallant&#x27;s Blog</a></li>

</ul>
</details>

**Tags**: `#Rust`, `#datetime`, `#libraries`, `#open source`, `#software engineering`

---

<a id="item-tech-news-3"></a>
### [Optimizely reportedly compromised, served malware via customer sites including Zoom and GitLab](https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/) ⭐️ 8.0/10

Optimizely, a widely used third-party experimentation and script vendor, was reportedly compromised and used to deliver malicious code through customer websites including Zoom and GitLab, according to a report-uri blog post. The report states that it is unknown how the attacker obtained write access to so many unrelated customer projects — whether through a compromised Optimizely system, a credential with cross-customer access, or something else — and that Optimizely&\#x27;s CDN served what it was given rather than being cache-poisoned. Optimizely&\#x27;s own properties, including www.optimizely.com and login.optimizely.com, also carried the injected code. The root cause and the full list of affected sites remain incompletely explained.

hackernews · kristjansson · Nov 16, 23:00 · [Discussion](https://news.ycombinator.com/item?id=50524767)

**「Background」** Optimizely is a third-party experimentation and optimization vendor whose JavaScript snippet customers embed directly into their own pages, so changes to experiments and page content can ship without the site&\#x27;s engineering team rebuilding anything. That arrangement means visitors to every embedding site execute whatever the vendor&\#x27;s delivery infrastructure returns. As quoted in the discussion, the report states that Optimizely&\#x27;s CDN served exactly what it was given — this was not cache poisoning — and that the malicious code also appeared in the snippets for www.optimizely.com and login.optimizely.com, while the mechanism by which the attacker obtained write access to unrelated customer projects remains unexplained.

**「Audit affected pages」** Organizations running Optimizely Web Experimentation must audit their pages for the injected script and confirm its removal rather than assume the vendor-side fix alone clears visitor exposure: the reported scope covers 178 organizations and 188 infected JavaScript files. Optimizely says it contained the incident, blocked the vulnerable path, removed the injected code, and contacted affected customers, but sites that loaded the compromised script still need to assess what their visitors executed.

**「Community discussion」** Commenters focused on the structural risk of third-party JavaScript: stickfigure argued that Google Tag Manager&\#x27;s original premise — letting marketing add tags without engineering involvement — is how news articles ended up loading roughly 10MB of JavaScript, and said teams should re-evaluate that practice. mcoliver called the incident avoidable and blamed a lack of accountability, proposing that large sites vendor such scripts rather than load them from vendors, while skybrian noted a missing step in the explanation: why sites like CNN and the BBC would handle cryptocurrency or credit cards on the same page at all.

<details><summary>References</summary>
<ul>
<li><a href="https://cybersecuritynews.com/optimizely-websites-hijacked/">Hackers Infect 178 Major Websites via Optimizely to Steal ...</a></li>
<li><a href="https://osintsights.com/optimizely-supply-chain-compromised-malware-hits-major-sites">Optimizely Supply Chain Compromised, Malware Hits Major Sites</a></li>
<li><a href="https://blog.redsidesecurity.com/post/optimizely-supply-chain-attack-injects-malicious-javascript-into-178-major-websites">Optimizely Supply-Chain Attack Hits 178 Major Websites</a></li>

</ul>
</details>

**Tags**: `#supply chain security`, `#third-party scripts`, `#web security`, `#Optimizely`, `#malware`

---

<a id="item-tech-news-4"></a>
### [US extends AI chip export controls to remote access](https://www.reuters.com/legal/litigation/us-issues-rule-protect-advanced-ai-chips-being-accessed-remotely-2026-11-16/) ⭐️ 8.0/10

The US Commerce Department issued an interim final rule on November 16 extending export controls on advanced AI chips and servers to remote access, aiming to stop users from circumventing restrictions through data centers in third countries. The rule was drafted under the leadership of the Treasury Department and the National Security Council, according to the source, and could further narrow China&\#x27;s routes to advanced chips. The Verge reported that the rule also requires licenses for re-exports of AI chips to Indonesia, Malaysia, Singapore, Thailand and Brazil. The source summary gives no effective date, licensing criteria, or technical thresholds for what counts as remote access.

telegram · zaihuapd · Nov 16, 14:44

**「Background」** The rule addresses a gap in earlier U.S. export controls that focused on shipping advanced AI chips and servers to restricted destinations. Foreign data centers could host such hardware and provide remote access to restricted users, which the new interim final rule now covers, including licensing requirements for re-exports to Indonesia, Malaysia, Singapore, Thailand and Brazil.

**「Compliance burden for third-country data centers」** Operators of data centers in Brazil, Singapore, Indonesia, Malaysia and Thailand must now obtain a US license before re-exporting advanced AI chips or providing remote access to them, according to reports on the interim final rule. That adds a licensing step that could delay or block existing third-country compute arrangements used by Chinese companies, as Bloomberg describes the rule&\#x27;s intent. Because the measure is an interim final rule, how licensing will treat specific remote-access setups remains to be tested in practice.

<details><summary>References</summary>
<ul>
<li><a href="https://wccftech.com/the-u-s-shuts-chinas-access-to-advanced-chips-via-singapore-brazil-indonesia-malaysia-and-thailand-as-scott-bessent-gives-nvidia-10-days-to-show-it-did-not-goose-its-revenues/">The U . S . Shuts China&#x27;s Access To Advanced Chips Via Singapore ...</a></li>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-16/us-moves-to-limit-remote-access-to-advanced-ai-chips">US Moves to Curb China’s Remote Access to Nvidia’s AI Chips</a></li>
<li><a href="https://qz.com/us-ai-chip-reexport-licenses-five-countries-111626">U . S . is requiring licenses to reexport AI chips to five countries</a></li>

</ul>
</details>

**Tags**: `#AI chip export controls`, `#US semiconductor policy`, `#remote access`, `#data centers`, `#AI hardware`

---

<a id="item-tech-news-5"></a>
### [Carnegie Mellon Launches CS Learn With Free Full-Semester Lectures on YouTube](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

Carnegie Mellon&\#x27;s Griffin School of Computer Science launched CS Learn, which publishes full semesters of lectures from current CMU computer science courses on YouTube for free, with one course premiering each day during launch week and more courses promised for January. Phillip Compeau, who runs the program, said a few CMU students built tools that automate much of the production work, allowing a small team to release the material. The initial catalog spans topics including machine learning systems and probability and computing. Lectures are the first piece; Compeau&\#x27;s comments indicate courseware is planned to follow, so projects and feedback mechanisms are not part of the launch.

hackernews · pcompeau · Nov 16, 20:43 · [Discussion](https://news.ycombinator.com/item?id=50522980)

**「Background」** MIT OpenCourseWare has long published materials from thousands of MIT courses online for free, establishing a widely known model for university open courseware. Carnegie Mellon&\#x27;s CS Learn is a later entry in that same free-course-materials tradition, offering full-semester lectures from current courses.

**「Impact」** Self-learners get current, full-length CMU lectures without enrollment or cost, but the launch is video-only for now, so learners who need problem sets, projects, or graded feedback must wait for the courseware component or supply their own practice. Compeau&\#x27;s description of student-built automation also suggests the release pace depends on a small team rather than a large production staff.

**「Community Discussion」** Commenters welcomed specific titles, with one CMU alum citing Tianqi Chen&\#x27;s ML Systems course and another praising 15-259 Probability and Computing, while requesting additional courses such as distributed systems, operating systems, and intermediate statistics. A recurring concern, raised by ecshafer, was that lectures without projects, notes, and feedback can fall flat, and that such releases often post introductory courses while skipping advanced ones like graduate compilers; another commenter argued that learning fundamentals well is what makes AI a power tool rather than a replacement.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/MIT_OpenCourseWare">MIT OpenCourseWare - Wikipedia</a></li>
<li><a href="https://ocw.mit.edu/">MIT OpenCourseWare | Free Online Course Materials</a></li>

</ul>
</details>

**Tags**: `#computer science education`, `#open courseware`, `#CMU`, `#machine learning systems`, `#YouTube`

---

<a id="item-tech-news-6"></a>
### [Windows 11 Reportedly Tracks Coding Agents and Developer Tools via Telemetry](https://xusheng.dev/posts/windows-coding-agent-telemetry/) ⭐️ 7.0/10

A report on xusheng.dev alleges that Windows 11 collects data on which coding agents and developer tools users run. A commenter summarizing the post says the information can be sent when the &quot;optimal&quot; diagnostics setting is enabled—claimed to be the default—and can be turned off via Settings → Privacy &amp; security → Diagnostics &amp; feedback. The supplied material does not name the specific data fields or independently verify the default setting.

hackernews · cwaffles · Nov 16, 22:58 · [Discussion](https://news.ycombinator.com/item?id=50524736)

**「Background」** Windows has long shipped Event Tracing for Windows \(ETW\), a built-in logging facility that components use to record diagnostic events; the developer-tool data described here is produced by a component called MissionControlAggregator rather than by a separate tracker. Coverage of Xusheng Li&\#x27;s November 16, 2026 write-up reports that the component generates a compact usage bitmap of which tools ran, not a transcript of coding sessions, and that no prompts were found. In the U.S. setup the investigator tested, optional diagnostic data was already enabled.

**「Opt-out action for developers」** Developers on Windows 11 who run coding agents or other developer tools should review Settings → Privacy &amp; security → Diagnostics &amp; feedback, because optional diagnostic data, described as default-on, can include which development tools are used. Turning off optional diagnostics is the concrete opt-out for users who do not want that tool-usage data sent to Microsoft.

**「Community Discussion」** Commenters disagree on the significance: some present Linux as a practical alternative after about a week of adjustment, while others argue comparable telemetry already exists in GPU drivers, Chrome, and Debian&\#x27;s popularity contest. One developer argues non-invasive telemetry is needed to prioritize agent sandboxing, noting that the MXC sandbox launched on Oct. 7 and Claude Code does not yet support it, leaving agents unsandboxed or run through WSL.

<details><summary>References</summary>
<ul>
<li><a href="https://windowsforum.com/news/windows-11-optional-telemetry-can-report-coding-agent-usage-research-finds.452631/">Windows 11 Optional Telemetry Can Report Coding Agent Usage ...</a></li>
<li><a href="https://news.lavx.hu/article/windows-11-collects-data-on-coding-agents-and-developer-tools-you-use">Windows 11 Collects Data on Coding Agents and Developer Tools ...</a></li>

</ul>
</details>

**Tags**: `#Windows 11`, `#telemetry`, `#privacy`, `#developer tools`, `#AI coding agents`

---

<a id="item-tech-news-7"></a>
### [Linebender wiki page covers squircle geometry for graphics](https://linebender.org/wiki/curves/squircle/) ⭐️ 7.0/10

Linebender&\#x27;s wiki hosts a technical reference article on squircles — the continuously curved rounded-rectangle shapes used in UI and graphics work — and the related curve geometry behind them. The page was posted to Hacker News by raphlinus and is an evergreen reference rather than a release announcement, with no version, API, or availability details attached. Readers should treat it as background material on curve construction, not as a shipped capability or a vendor claim about a specific product.

hackernews · raphlinus · Nov 16, 07:55 · [Discussion](https://news.ycombinator.com/item?id=50515151)

**「Background」** A squircle is a shape between a square and a circle, formally a superellipse, whose curvature transitions smoothly rather than breaking at a corner — the property that makes such curves useful when a shape must meet physical or interactive rendering. The article sits in the curves wiki of Linebender, a group focused on 2D graphics and user interface design whose projects are mostly written in Rust.

**「Impact」** For developers choosing how to draw rounded corners, the discussion centers on derivative continuity: one commenter argues that curves without discontinuities in their derivatives are exactly what enable perceived smoothness once a shape meets physical interaction, which is the practical difference between squircle-style corners and plain circular arcs. A commenter building a spline-authoring tool reports that superellipses and clothoids feature heavily in it, suggesting the geometry described in the article is already being applied in early-stage authoring tools rather than only in finished UI frameworks.

**「Community discussion」** Commenters traded practical examples rather than debating the article&\#x27;s math: one praised the Zune 2nd-generation model&\#x27;s squircle d-pad as feeling like a mini touchpad without a cursor, and another pointed to the three-dimensional analogue, the &quot;sphube,&quot; with a linked arXiv paper. A developer shared an in-progress spline and superellipse authoring demo at thiic.cc/omnispline/, describing it as a stack of edge-case exceptions still in the exploration stage.

<details><summary>References</summary>
<ul>
<li><a href="https://linebender.org/">Homepage for the Linebender organization</a></li>

</ul>
</details>

**Tags**: `#computer graphics`, `#UI design`, `#geometry`, `#curves`, `#splines`

---

<a id="item-tech-news-8"></a>
### [Microsoft blames major email outage on July fix defect](https://www.theregister.com/saas/2026/11/16/microsoft-blames-monster-email-outage-on-software-defect-introduced-in-july-fix/5310026) ⭐️ 7.0/10

Microsoft has blamed a major email outage on a software defect introduced by a fix it shipped in July, according to The Register. The report describes the disruption as a large-scale email failure but, in the supplied material, does not identify the specific service, outage duration, number of affected users, or the code change at fault. Microsoft’s attribution makes the July update the stated root cause; independent confirmation and a full postmortem were not available in the source excerpt.

hackernews · Bender · Nov 16, 13:18 · [Discussion](https://news.ycombinator.com/item?id=50517321)

**「Background」** The outage had already left Outlook unavailable for more than 12 hours by November 12, when NPR reported that millions of individuals and organizations, including its newsroom, had lost access and that Microsoft was claiming only &quot;marginal success&quot; in recovery. Microsoft&\#x27;s later incident report said the defective change had been deployed to Microsoft 365 networking gateway servers in July and ran globally for more than three months without visible problems.

**「Operational fallout」** Organizations that route critical communications through Outlook lost email access for hours, with effects reported in more than 70 countries and disruptions reaching hospitals, schools, businesses and Congressional offices, as well as Microsoft&\#x27;s own staff. Because the defect entered through a July fix rather than a fresh deployment, teams whose continuity plans treat only new changes as risky should treat vendor patches as potential incident sources and keep out-of-band contact channels available.

**「Community discussion」** Commenters focused on recovery mechanics and testing gaps: one compared the recovery to a grid “black start,” while another asked why Microsoft could not shed load by limiting connections to rotating IP ranges. Others questioned why Windows was used for critical network infrastructure and whether it is acceptable for a concurrency bug to pass in a low-end test environment that differed from production.

<details><summary>References</summary>
<ul>
<li><a href="https://www.npr.org/2026/11/12/nx-s1-6039343/outlook-down-widespread-outage-microsoft-email">A negative Outlook: Microsoft scrambles to fix email outage : NPR</a></li>
<li><a href="https://cybersecuritynews.com/microsoft-outage-incident-report/">Microsoft Reveals How a Hidden Windows Bug Took Down Microsoft ...</a></li>
<li><a href="https://www.npr.org/2026/11/12/nx-s1-6039343/outlook-down-widespread-outage-microsoft-email">A negative Outlook: Microsoft scrambles to fix email outage : NPR</a></li>
<li><a href="https://www.nytimes.com/2026/11/13/business/microsoft-outage.html">Inside Microsoft ’s Rush to Get Back Online After a Global Outage</a></li>

</ul>
</details>

**Tags**: `#Microsoft`, `#email outage`, `#incident postmortem`, `#site reliability`, `#software defect`

---

<a id="item-tech-news-9"></a>
### [Marimba uses one frozen Qwen3-ASR pass for typed audio queries](https://www.reddit.com/r/MachineLearning/comments/1xxsqro/marimba_a_system_one_model_for_speech_r/) ⭐️ 7.0/10

A Reddit research announcement and linked arXiv paper describe Marimba, a speech system that answers typed yes/no, multiple-choice, or score questions about an 8-second audio window and returns a calibrated probability from a single frozen Qwen3-ASR-0.6B encoder pass. The authors report that on the same 1,000 public questions it matches or beats Qwen3-Omni \(30B-A3B\) on 6 of 9 tests, while Qwen3-Omni remains better on Speech Commands. They also report 100% language identification on 300 FLEURS clips, speaker-change AUROC of 0.966–0.980 on AMI and VoxConverse, and speaker count above pyannote 3.1. The caveats are substantial: the turn-end readout was trained on Smart Turn data, scores 0.930 AUROC versus Smart Turn v3.2 at 0.982 on Smart Turn&\#x27;s own test set, ties on ICSI meetings at 0.716 versus 0.712, and every head is at chance on CochlScene scene classification.

reddit · r/MachineLearning · /u/solanotodesch · Nov 16, 15:47

**「Background」** The post says Marimba follows up on the author&\#x27;s Reddit announcement from the previous week and now adds the arXiv paper, GitHub code, Apache-2.0 Hugging Face weights, a demo, and a pip package. Its setup depends on a frozen Qwen3-ASR-0.6B encoder, with question-specific readouts or calibrated ASR-hypothesis scoring built on a single encoder pass per 8-second audio window.

**「Impact」** Developers can test the Apache-2.0 weights via the \`marimba-audio\` package, the GitHub repository, and a Hugging Face demo, but should validate turn-end detection on their own audio rather than assume the reported results transfer: the turn-end readout was trained on Smart Turn data and underperformed Smart Turn v3.2 on that model&\#x27;s own test set.

**Tags**: `#speech recognition`, `#audio models`, `#efficient inference`, `#model calibration`, `#Qwen3-ASR`

---

<a id="item-tech-news-10"></a>
### [Duetto steers a pretrained music transformer into a real-time jazz partner](https://www.reddit.com/r/MachineLearning/comments/1xxkyh3/steering_a_pretrained_music_transformer_at/) ⭐️ 7.0/10

A developer has released duetto, a real-time MIDI jazz partner that plays alongside a keyboardist as a small band—solo, comping, and walking bass—and takes a solo when the player stops. Instead of fine-tuning, duetto uses the pretrained Anticipatory Music Transformer \(Thickstun et al., 2023\) unchanged and controls generation at sampling time by masking and biasing logits before each note, represented as onset, duration, and pitch. In a 160 bpm “Autumn Leaves” demo, about 61% of solo notes came from quoted Weimar Jazz Database phrases or the theme and the rest from the model, while the server kept about one second of music sampled ahead and resampled the unplayed part when the player played, according to the author. The author reports about 12 ms/note for the medium model and 18 ms/note for the large model on a 3080 Ti, and about 90 ms/note for the large model on a Jetson Orin Nano; there is no independent evaluation, and the author notes drift from the player and a fragile balance between model ideas and rule-based guidance.

reddit · r/MachineLearning · /u/GGAllin43 · Nov 16, 09:19

**「The pretrained model behind it」** Duetto runs the Anticipatory Music Transformer as released, without training it. That model, published in June 2023 by Thickstun, Hall, Donahue, and Liang, is trained with an &quot;anticipation&quot; objective so it can infill around existing musical events rather than only continue a prompt, and the authors demonstrated that capability on accompaniment tasks; human evaluators rated its 20-second accompaniments as similar in musicality to human-composed ones. Pretrained weights and sampling code are publicly available through CRFM and the project&\#x27;s GitHub repository under Apache 2.0, which is what makes a no-fine-tuning build possible.

**「Impact」** For live symbolic-music systems, the reported ~90 ms/note for the large model on a Jetson Orin Nano indicates the sampling-time steering approach can run on edge hardware without fine-tuning, but the author&\#x27;s noted drift and fragile bias balance mean it remains a prototype rather than a dependable accompanist.

<details><summary>References</summary>
<ul>
<li><a href="https://arxiv.org/abs/2306.08620">[2306.08620] Anticipatory Music Transformer - arXiv.org</a></li>
<li><a href="https://crfm.stanford.edu/2023/06/16/anticipatory-music-transformer.html">Anticipatory Music Transformer: A Controllable Infilling ...</a></li>
<li><a href="https://github.com/jthickstun/anticipation">GitHub - jthickstun/anticipation: Anticipatory Autoregressive ... Anticipatory Music Transformer - arXiv.org Anticipation and the Anticipatory Music Transformer (PDF) Anticipatory Music Transformer - ResearchGate Anticipatory Music Transformer - John Thickstun</a></li>

</ul>
</details>

**Tags**: `#music-generation`, `#transformer`, `#inference-time-steering`, `#real-time-music`, `#pretrained-models`

---

<a id="item-tech-news-11"></a>
### [US and nine countries sign San Francisco Declaration on AI supply chains](https://www.state.gov/releases/office-of-the-spokesman/2026/11/the-san-francisco-declaration-on-the-secure-foundations-of-enduring-prosperity/) ⭐️ 7.0/10

On November 15, the United States and nine other countries — Australia, India, Israel, Japan, South Korea, Qatar, Singapore, the UAE, and the United Kingdom — signed the San Francisco Declaration, which states that economic security underpins national security and commits the signatories to jointly protect sensitive technologies and critical infrastructure supporting the superintelligence \(SI\) supply chain. The declaration establishes five working groups covering innovation policy frameworks, SI applications in critical sectors, full-stack SI supply chain collaboration, safe harbors and supply chain security hubs, and SI security and resilience. The supplied source describes the working groups&\#x27; mandates but does not list binding commitments, timelines, or specific technologies or controls. It is therefore a framework announcement rather than a detailed, enforceable agreement.

telegram · zaihuapd · Nov 16, 10:40

**「Context」** The declaration was signed at the Pax Silica Founders Retreat, convened by U.S. Under Secretary of State for Economic Affairs Jacob Helberg, according to reports on the State Department announcement. The participating governments framed the effort as a way to reduce reliance on U.S. adversaries for critical minerals, AI models, and semiconductor chips.

**「Impact」** The five working groups give the ten participating governments standing channels to coordinate on SI supply chain security, which is where export-control, procurement, and critical-infrastructure security expectations for companies operating in these countries are likely to be shaped. No specific compliance obligations are described in the source, so affected firms have no concrete new requirements to act on yet, but they should track the working groups&\#x27; outputs for future guidance.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/San_Francisco_Declaration_on_the_Secure_Foundations_of_Enduring_Prosperity">San Francisco Declaration on the Secure Foundations of Enduring Prosperity</a></li>
<li><a href="https://www.investing.com/news/world-news/us-nine-nations-sign-san-francisco-declaration-on-ai-security-5028448">U.S., nine nations sign San Francisco declaration on AI security By...</a></li>

</ul>
</details>

**Tags**: `#AI policy`, `#AI supply chain`, `#international agreement`, `#AI governance`, `#critical infrastructure`

---

<a id="item-tech-news-12"></a>
### [Amazon: Artex AI agents stole API keys to fund LLM use](https://cybernews.com/security/amazon-autonomous-cybercrime-artex-framework/) ⭐️ 7.0/10

Amazon says attackers used the open-source Artex penetration-testing framework to drive AI agents that stole API keys from internet-exposed AI applications, including LiteLLM and Dify, validated the keys, and pooled them to pay for additional LLM calls. The campaign began on October 3 and was blocked on November 5 by Amazon&\#x27;s MadPot decoy network, according to the report. Amazon attributes the activity to a China-related threat group with medium confidence, says not all listed targets were compromised, and has notified potentially affected AWS customers. The account is Amazon&\#x27;s assessment as summarized by Cybernews, with no independent confirmation provided in the source.

telegram · zaihuapd · Nov 16, 13:00

**「Background」** AI gateways such as LiteLLM and app-building platforms such as Dify store upstream model-provider API keys, so an internet-exposed instance can be valuable even without other sensitive data. Amazon&\#x27;s captured agent records, as reported by The Hacker News and Quartz, show the agents probing those products for known entry points and attempting to extract the provider keys stored inside.

**「Impact」** The immediate consequence falls on operators of internet-exposed LiteLLM and Dify deployments, which Amazon identifies as targets, because stolen keys were pooled to fund further model usage. Amazon says it notified potentially affected AWS customers and that not all listed targets were compromised, but the report names no affected customers or indicators of compromise.

<details><summary>References</summary>
<ul>
<li><a href="https://thehackernews.com/2026/11/amazon-uncovers-ai-agent-campaign.html">Amazon Uncovers AI Agent Campaign Targeting LiteLLM , Dify , and...</a></li>
<li><a href="https://qz.com/amazon-ai-agents-steal-provider-keys-artex-111626">Amazon captured records of AI agents trying to steal AI keys</a></li>

</ul>
</details>

**Tags**: `#AI security`, `#autonomous agents`, `#API key theft`, `#cybercrime`, `#AWS`

---

<a id="item-tech-news-13"></a>
### [Alibaba, Tencent, Moonshot Reportedly Curb Cyber Capabilities; Qwen Flagship Withholds Open Weights](https://www.bloomberg.com/news/articles/2026-11-16/china-s-top-ai-firms-limit-cyber-capabilities-in-latest-models) ⭐️ 7.0/10

Bloomberg reported that Alibaba, Tencent and Moonshot weakened offensive cyber capabilities in their newest models while improving defensive performance, amid draft export-control measures published by China&\#x27;s Commerce Ministry last month. Those draft rules would bar exports of AI tools capable of attacking critical infrastructure or government networks. Alibaba&\#x27;s latest flagship Qwen was not released with open weights, so users cannot download and customize the full model; Tencent reportedly cut cyber functions before releasing Hy4 this month.

telegram · zaihuapd · Nov 17, 02:20

**「Background」** Open-weight releases let users download and modify a model’s full parameters, while closed models remain available only through vendor-controlled access. The reported curbs also follow a draft export-control rule that China’s Commerce Ministry published the previous month, which would bar exports of AI tools capable of attacking critical infrastructure or government networks.

**「Impact」** Developers and researchers who build on downloadable Qwen weights cannot fine-tune or self-host the latest flagship, and organizations deploying Chinese models should expect reduced offensive-cyber functionality alongside claimed stronger defenses.

**Tags**: `#AI policy`, `#cybersecurity`, `#open-weight models`, `#China AI`, `#export controls`

---

## Financial News

<a id="item-finance-news-1"></a>
### [CNBC: Lutnick&\#x27;s sons&\#x27; firm cut Nvidia stake amid chip-smuggling scrutiny](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

CNBC reported that Cantor Fitzgerald — the Wall Street firm formerly run by Commerce Secretary Howard Lutnick and now led by his sons Brandon and Kyle — cut the number of Nvidia shares it reported holding by 49% between September 2025 and March 2026, from about 3.5 million shares worth $652 million to 1.78 million shares worth $310 million, as Lutnick faced pressure over suspected smuggling of Nvidia AI chips to China. CNBC said there is no evidence the holdings changes were tied to intelligence warnings about Nvidia CEO Jensen Huang or that the firm&\#x27;s business interests influenced Lutnick&\#x27;s decisions, and Cantor said its Nvidia positions were immaterial and arose from client swap transactions.

rss · CNBC Finance · Nov 16, 12:14

**「Background」** Howard Lutnick left Cantor Fitzgerald, the Wall Street firm now led by his sons, to become commerce secretary in February 2025, putting him in charge of the department that enforces U.S. export controls, including the entity list of restricted companies.

**Tags**: `#Nvidia`, `#US-China export controls`, `#conflict of interest`, `#Commerce Department`, `#corporate governance`

---

<a id="item-finance-news-2"></a>
### [Intel and CEO Lip-Bu Tan sued by shareholders after stock plunge](https://www.investing.com/news/stock-market-news/intel-sued-by-shareholders-following-29-stock-plunge-5028171) ⭐️ 7.0/10

Intel and CEO Lip-Bu Tan, along with CFO David Zinsner, were sued by shareholders in a proposed class action filed Friday in San Jose federal court, accusing the company of concealing weak PC demand and a build-up of inventory. The suit followed Intel&\#x27;s October 29 fourth-quarter revenue and profit forecast, which fell short of expectations, and a 28.6% share-price drop the next day that erased about $140 billion in market value, according to Reuters.

telegram · zaihuapd · Nov 16, 11:10

**「Background」** The proposed class action, filed in San Jose federal court under the Securities Exchange Act of 1934, covers investors who bought Intel shares from July 23 to Oct. 29, 2026, and names CEO Lip-Bu Tan and CFO David Zinsner as defendants alongside the company. It follows Intel’s weak fourth-quarter revenue forecast on Oct. 29, after which the stock fell 28.6% the next day.

**「Who is affected」** The Michigan pension fund leading the case seeks to represent investors who bought Intel stock between July 23 and October 29, 2026, the period the suit says the alleged omissions affected.

<details><summary>References</summary>
<ul>
<li><a href="https://finance.yahoo.com/markets/stocks/articles/why-intel-facing-shareholder-lawsuit-143331644.html?fr=sycsrp_catchall">Why Is Intel Facing a Shareholder Lawsuit Over Its PC Slowdown?</a></li>
<li><a href="https://www.bbc.com/news/articles/cw62p42p288do">Investors sue chip giant Intel after 29% stock plunge - BBC</a></li>

</ul>
</details>

**Tags**: `#Intel`, `#shareholder lawsuit`, `#semiconductor`, `#stock plunge`, `#earnings warning`

---