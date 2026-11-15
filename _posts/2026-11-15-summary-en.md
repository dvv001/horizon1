---
layout: default
title: "Horizon Summary: 2026-11-15 (EN)"
date: 2026-11-15
lang: en
---

> From 39 items, 8 important content pieces were selected

---

**Technology News**
1. [SpaceX catches Starship upper stage on Flight 15, booster misses](#item-tech-news-1) ⭐️ 8.0/10
2. [Lovable apps alleged to expose passport data, 200K messages via RLS gaps](#item-tech-news-2) ⭐️ 8.0/10
3. [Show HN: DeepSeek V3 reimplemented in ~200 lines of pure JAX](#item-tech-news-3) ⭐️ 7.0/10
4. [EFF says tech companies are trying to redefine privacy again](#item-tech-news-4) ⭐️ 7.0/10
5. [Project Zero moves to 90-day vulnerability disclosure, with shorter deadlines planned](#item-tech-news-5) ⭐️ 7.0/10
6. [Cloudflare open-sources Kitesurf, an Apache-2.0 stateless browser for AI agents](#item-tech-news-6) ⭐️ 7.0/10
7. [Tesla Cybercab terms reportedly require $299 monthly fee to drive](#item-tech-news-7) ⭐️ 7.0/10

**Financial News**
1. [Anthropic IPO reportedly bars mainland China and Hong Kong investors](#item-finance-news-1) ⭐️ 8.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [SpaceX catches Starship upper stage on Flight 15, booster misses](https://www.spacex.com/launches/starship-flight-15) ⭐️ 8.0/10

SpaceX&\#x27;s Starship Flight 15 ended with the first tower-arm catch of the orbital-class ship after about 22.5 hours in space and roughly 14 orbits, SpaceX announced. The ship also deployed all 26 Starlink V3 satellites. The Super Heavy booster did not return to the launch tower and instead splashed down in the Gulf of Mexico, so SpaceX missed the planned dual catch and has not yet demonstrated recovering both stages on one flight.

hackernews · ls612 · Nov 14, 21:22 · [Discussion](https://news.ycombinator.com/item?id=50500963)

**「Tower-catch recovery」** SpaceX’s “tower catch” recovery method uses the launch tower’s mechanical arms to grip a returning vehicle at a designated catch point instead of having it land on legs or splash down. Flight 15 was the 15th Starship test and had planned to catch both the booster and ship, but the booster aborted its return and splashed down in the Gulf of Mexico while the ship completed the first orbital-class ship catch.

**「Impact」** The immediate next milestone is reusing a recovered ship and eventually catching the booster as well; until both are demonstrated, Flight 15 does not establish the two-stage reuse that SpaceX&\#x27;s launch-cost case depends on.

**「Community discussion」** Commenters treated the ship catch as the key step toward full reuse, but several emphasized that the remaining proof is heat-shield survival, re-flying the same vehicles, and a future double catch. One commenter described Starship as a corrected Space Shuttle, while another estimated Falcon 9&\#x27;s booster and fairings at about 60% of launch cost—arguments offered in support of full reusability rather than independent findings.

**Tags**: `#SpaceX`, `#Starship`, `#reusable rockets`, `#aerospace engineering`, `#spaceflight`

---

<a id="item-tech-news-2"></a>
### [Lovable apps alleged to expose passport data, 200K messages via RLS gaps](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

A security research post on crissyfield.de alleges that apps built with Lovable exposed passport details and more than 200,000 private messages through insufficient Row-Level Security. Lovable&\#x27;s head of security, posting as igorandri, acknowledged in the discussion that insufficient RLS was the root cause, saying Lovable scans every app automatically before publish and offers a free deeper SAST scan, with “Fix” and auto-fix options. The post&\#x27;s author also joined the thread; the supplied material does not state how many apps or users were affected.

hackernews · armcat · Nov 14, 17:43 · [Discussion](https://news.ycombinator.com/item?id=50499017)

**「Why RLS defaults matter here」** Lovable-built apps typically sit on Supabase, where Postgres Row-Level Security enforces authorization inside the database; Supabase&\#x27;s documentation states that a table in an exposed schema without RLS is readable and writable by any role holding a grant on it. Supabase&\#x27;s Data API historically exposed public-schema tables automatically, and write-ups of the platform&\#x27;s October 30, 2026 change say new tables created in the public schema are no longer reachable through the REST and GraphQL APIs by default.

**「Impact」** Developers shipping Lovable apps should treat RLS policy review as a release gate, checking every table and API path rather than relying on a clean publish scan; the reported cases involve apps that were already exposing data, while Lovable says its scanner and optional SAST can flag findings for users to fix.

**「Community discussion」** Commenters dispute where responsibility lies: one argues that Supabase&\#x27;s historical defaults are a major factor and claims existing projects may still carry them after what they describe as an October 30 fix, while another says AI-generated apps mainly change the scale and ease of exploitation rather than creating a new kind of breach. Lovable&\#x27;s head of security and the post&\#x27;s author both participated, with the vendor describing pre-publish scanning and auto-fix controls.

<details><summary>References</summary>
<ul>
<li><a href="https://supabase.com/docs/guides/database/postgres/row-level-security">Row Level Security - Supabase Docs</a></li>
<li><a href="https://rlsradar.vercel.app/guides/supabase-data-api-change-oct-30-2026.html">Supabase Oct 30, 2026 Data API change: what it means for RLS</a></li>

</ul>
</details>

**Tags**: `#security`, `#AI app builders`, `#Supabase`, `#Row-Level Security`, `#vulnerability disclosure`

---

<a id="item-tech-news-3"></a>
### [Show HN: DeepSeek V3 reimplemented in ~200 lines of pure JAX](https://github.com/Vaibhaav-Tiwari/deepseek-v3-jax) ⭐️ 7.0/10

A Show HN post by VaibhaavTiwari presents a from-scratch JAX implementation of DeepSeek V3, described as roughly 200 lines of pure JAX. The linked GitHub repository is framed as a compact educational reconstruction of the model rather than an official release or a benchmarking effort. No source content was supplied with the item, so the implementation&\#x27;s completeness, supported weight formats, and inference performance are not established here; the line count and scope come from the author&\#x27;s own description.

hackernews · VaibhaavTiwari · Nov 14, 15:04 · [Discussion](https://news.ycombinator.com/item?id=50497589)

**「What DeepSeek V3&\#x27;s architecture involves」** DeepSeek V3 is a Mixture-of-Experts \(MoE\) language model with 671B total parameters, only about 37B of which are activated for each token \(tool-2-1, tool-2-2\). That sparse routing keeps per-token compute well below the full parameter count, while memory still scales with the total model size \(tool-2-3\). A compact from-scratch JAX implementation therefore has to reproduce the expert-routing and layer structure, not just a dense transformer.

**「Practical note for AMD users」** One commenter reported that the project was the first to run end-to-end for local work on an AMD RX 7600 XT 16GB under Fedora with ROCm, using JAX rather than CUDA, and noted that it required setting HSA\_OVERRIDE\_GFX\_VERSION=11.0.0 because JAX&\#x27;s plugin rejects the card&\#x27;s gfx1102 target. That is a single user&\#x27;s reported setup, not a verified compatibility guarantee; readers on similar RDNA3 cards should expect to set the override variable before attempting to run it.

**「Community reaction」** Commenters generally welcomed the project as a way to learn LLM internals from first principles, with one saying they plan to recreate it for study and another asking for a roadmap for engineers comfortable with Python or Java but new to inference. The most substantive report was the ROCm/AMD setup experience, which was offered as troubleshooting detail rather than independent confirmation of the code&\#x27;s correctness.

<details><summary>References</summary>
<ul>
<li><a href="https://huggingface.co/deepseek-ai/DeepSeek-V3-Base">deepseek -ai/ DeepSeek - V 3 -Base · Hugging Face</a></li>
<li><a href="https://dev.to/jamilxt/mixture-of-experts-moe-why-big-ai-models-are-cheaper-to-run-than-they-look-2g6i">Mixture of Experts (MoE): Why Big AI Models Are... - DEV Community</a></li>
<li><a href="https://www.linkedin.com/pulse/mixture-experts-architecture-quietly-running-most-sundaravaradan-ygfyc">Mixture of Experts — the architecture quietly running most of the...</a></li>

</ul>
</details>

**Tags**: `#JAX`, `#DeepSeek V3`, `#LLM inference`, `#ROCm`, `#minimal implementation`

---

<a id="item-tech-news-4"></a>
### [EFF says tech companies are trying to redefine privacy again](https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again) ⭐️ 7.0/10

EFF published a policy analysis arguing that technology companies are once again trying to shift the entire concept of privacy, framing the issue as corporate redefinition rather than a narrow product change. The available account does not name specific companies, proposals, or legislative text, so it is an advocacy argument about framing, not a report on a particular shipped feature or rule. The accompanying discussion focused on AI meeting notetakers, accessibility, and whether recording is becoming an unavoidable workplace default.

hackernews · gslin · Nov 14, 12:45 · [Discussion](https://news.ycombinator.com/item?id=50496602)

**「Background」** The piece lands amid a wave of always-on wearable capture marketed as everyday convenience: Meta and Google smart glasses that can record what the wearer sees and have AI describe it, Apple&\#x27;s Audio Intelligence turning the Apple Watch into a transcription device, and Amazon&\#x27;s Bee devices recording and transcribing continuously. Critics group these under &quot;ambient surveillance,&quot; where the person being recorded is usually a bystander who never chose the device.

**「Impact」** For workers, the practical concern raised in the discussion is that AI notetakers can become a meeting default that individuals cannot easily refuse without social or employment cost. That makes opt-out a matter of workplace norms and power, not merely a product setting.

**「Community discussion」** Commenters described AI notetakers as increasingly unavoidable in professional meetings, with one asking whether it is realistic to establish a norm of saying transcription is not needed before a meeting proceeds. Another argued that live transcription can be transformative for deaf and hard-of-hearing users and could run on a local model without retention, framing accessibility as a reason not to treat the technology itself as the sole problem.

<details><summary>References</summary>
<ul>
<li><a href="https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again">Tech Companies Are Trying to Shift the Entire Concept of ...</a></li>
<li><a href="https://zerodaily.in/a/92b01cf9">Tech Companies Are Trying to Shift the Concept of Privacy ...</a></li>

</ul>
</details>

**Tags**: `#privacy`, `#AI surveillance`, `#digital rights`, `#tech policy`, `#AI notetakers`

---

<a id="item-tech-news-5"></a>
### [Project Zero moves to 90-day vulnerability disclosure, with shorter deadlines planned](https://projectzero.google/2026/11/disclosure-policy.html) ⭐️ 7.0/10

Google Project Zero will disclose vulnerabilities 90 days after they are reported, according to the item, with a staged reduction to shorter deadlines described in the discussion. A comment quoting the policy says the 90-day &quot;Full 90&quot; rule starts now, followed by a 60-day deadline on February 2, 2027, and a 30-day deadline on January 3, 2028. The supplied item did not include the announcement text, so the exact scope, exceptions, and vendor-coordination terms are unconfirmed.

hackernews · hacb · Nov 14, 11:13 · [Discussion](https://news.ycombinator.com/item?id=50496051)

**「Background」** A vulnerability disclosure deadline is the private window a reporter gives a vendor or maintainer before publishing technical details, so its length largely determines whether a fix can ship before the bug becomes public. Project Zero&\#x27;s quoted policy turns that window into a fixed countdown — 90 days now, with further reductions to 60 and then 30 days scheduled for February 2027 and January 2028 — rather than a single open-ended timeline.

**「Impact」** The shortened window puts pressure on vendors, open-source maintainers, and downstream distributions to patch before details become public; one commenter specifically warned that Ubuntu would need &quot;a LOT more time&quot; than 90 days. That makes patch coordination, not just bug discovery, the practical bottleneck for organizations relying on slower release cycles.

**「Community discussion」** Commenters disagreed about whether the shorter deadline is appropriate: one argued for immediate disclosure because nothing else compels vendors to fix, while another said Ubuntu would need far more time than 90 days. Another commenter asked whether firms that find bugs should also give vendors and open-source projects access to the products used to discover them, warning that disclosure pressure could otherwise become a way to push LLM adoption.

**Tags**: `#vulnerability disclosure`, `#security policy`, `#Google Project Zero`, `#software maintenance`

---

<a id="item-tech-news-6"></a>
### [Cloudflare open-sources Kitesurf, an Apache-2.0 stateless browser for AI agents](https://www.phoronix.com/news/Cloudflare-Kitesurf-Open-Source) ⭐️ 7.0/10

Cloudflare has open-sourced Kitesurf under the Apache 2.0 license, a stateless browser aimed at AI agents that runs on Cloudflare Workers. According to the source, it parses HTML, handles CSS and executes JavaScript without requiring browser containers, and the code is published on GitHub. Cloudflare&\#x27;s stated goal is a lightweight, efficient browser for agents that uses less CPU and memory than Chromium and can scale on demand across its global Workers network. These performance and scaling figures are vendor claims; the source provides no architecture details or benchmarks, and no independent measurements.

telegram · zaihuapd · Nov 14, 09:33

**「Background」** AI agents that interact with websites generally need a browser engine such as Chromium, which is commonly run inside a container and consumes substantial CPU and memory. Kitesurf takes a different approach: it is built on Cloudflare Workers and described as stateless, parsing HTML, applying CSS, and executing JavaScript without a browser container.

**「Deployment constraints」** Adopting Kitesurf is not a drop-in swap for a Chromium-based automation stack: the GitHub repository states it requires Cloudflare Dynamic Workers to create isolated workers for pages, so deploying beyond a local run means hosting on Cloudflare&\#x27;s platform. Agents and other clients connect through Chrome DevTools Protocol endpoints, and Cloudflare describes the engine as experimental, so teams evaluating it should plan to keep existing headless-browser fallbacks.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.cloudflare.com/kitesurf-open-source/">Kitesurf is now open source | Cloudflare Blog</a></li>
<li><a href="https://github.com/cloudflare/kitesurf">GitHub - cloudflare / kitesurf : Kitesurf is an experimental browser ...</a></li>

</ul>
</details>

**Tags**: `#ai-agents`, `#open-source`, `#cloudflare-workers`, `#headless-browser`, `#web-automation`

---

<a id="item-tech-news-7"></a>
### [Tesla Cybercab terms reportedly require $299 monthly fee to drive](https://www.tesla.com/configurator/api/v4/terms?category=autonomy_subs&amp;amp;locale=en_US&amp;amp;model=cc&amp;amp;saleType=Sale) ⭐️ 7.0/10

The Cybercab subscription terms reported in the source item set the vehicle price at $29,990 and require a $299 monthly autonomy payment for the car to operate. Under the terms, Tesla can change the subscription price with one month&\#x27;s notice, and nonpayment or misuse can lead to suspension or cancellation; three cumulative warnings can disable autonomous driving for one week. Vehicles are restricted to designated areas, and unauthorized use on ride-hailing, delivery, or rental platforms is prohibited. Electrek noted that the Cybercab and the Model Y used for Robotaxi share AI4 hardware and autonomous-driving software, while FSD for ordinary owners still requires human supervision.

telegram · zaihuapd · Nov 15, 01:10

**「Background」** Tesla already offers FSD as a software feature for ordinary owners, but the report says that version still requires human supervision; its Robotaxi service uses Model Y vehicles with the same AI4 hardware and autonomous-driving software. The Cybercab agreement makes that software layer a condition of the vehicle operating at all, rather than an optional driver-assistance add-on.

**「Impact」** For prospective owners, the $29,990 purchase does not buy standalone operation: the $299 monthly payment is a condition of use, and missed payments or three cumulative warnings can suspend autonomous driving. The terms also bar unauthorized use on ride-hailing, delivery, or rental platforms, limiting how owners can deploy the vehicle commercially.

**Tags**: `#Tesla Cybercab`, `#autonomous vehicles`, `#subscription model`, `#FSD`, `#robotaxi`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Anthropic IPO reportedly bars mainland China and Hong Kong investors](https://m.economictimes.com/markets/us-stocks/news/anthropic-ipo-share-orders-from-china-are-said-to-be-rebuffed/articleshow/135809948.cms) ⭐️ 8.0/10

Anthropic&\#x27;s reported initial public offering is not accepting orders from mainland Chinese or Hong Kong investors, with people cited by the Economic Times linking the restriction to ITAR arms-export controls. The offering is reported to price on Nov. 18 ahead of a next-day listing under the ticker ANT, aiming to raise up to $90.4 billion at a $1.4 trillion valuation, with demand around six times the shares available.

telegram · zaihuapd · Nov 14, 10:18

**「Background」** Anthropic’s reported IPO is seeking a valuation of up to $1.4 trillion, according to Reuters, and the exclusion is tied to ITAR — US export-control rules covering military-related technology.

**「Impact」** Mainland Chinese and Hong Kong investors are barred from placing direct orders, and the report says some are routing demand through British Virgin Islands trusts, SPVs and swaps.

<details><summary>References</summary>
<ul>
<li><a href="https://www.reuters.com/business/anthropic-ipo-raise-much-644-billion-latest-draft-prospectus-shows-2026-11-10/">EXCLUSIVE: Anthropic eyes $1.4 trillion IPO valuation in test ...</a></li>

</ul>
</details>

**Tags**: `#Anthropic IPO`, `#China/Hong Kong investor restrictions`, `#ITAR export controls`, `#AI financing`, `#IPO demand`

---