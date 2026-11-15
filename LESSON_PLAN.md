# AI GTM Architect: সম্পূর্ণ Lesson Plan

> **লক্ষ্য:** একজন অভিজ্ঞ AI Engineer থেকে **AI + GTM Engineer**, তারপর **AI GTM Architect** হওয়া।
> **Flagship project:** Autonomous AI GTM Engine (প্রতিটা lesson এর tool এই engine এর একটা অংশ)।
> **Stack:** Python, FastAPI, LangGraph, PostgreSQL, Redis, HubSpot API, n8n

---

## প্রতিটা Lesson এর Format

প্রতিটা lesson এ (২০–৩০ মিনিট পড়া + build time) চারটা পর্ব থাকবে:

| পর্ব | কী থাকবে |
|---|---|
| **১. গল্প দিয়ে Theory** | Beginner level, বাংলায়, একটা বাস্তব গল্প দিয়ে concept। Technical term English এ। |
| **২. Q&A** | সাধারণ প্রশ্নের উত্তর + আমার জন্য ৩টা প্রশ্ন (একটা real business scenario সহ) |
| **৩. Tool পরিচিতি + Build** | Industry tool এর পরিচিতি + নিজের AI skill (inference, orchestration, structured output) দিয়ে একটা tool বানানো |
| **৪. Self-Branding** | LinkedIn/portfolio এর ছোট কাজ। **কখনো বানানো result বা অভিজ্ঞতা না।** |

প্রতিটা lesson এর শেষে একটা **Build Prompt** আছে। Claude Code বা অন্য AI coding tool এ দিলে tool এর skeleton শুরু করা যাবে। পুরো code AI কে দিয়ে লেখানো উদ্দেশ্য না: architecture decision, eval আর review নিজে করতে হবে।

### Lesson শেষ হয়েছে কখন বলবো? (Definition of Done)
- [ ] Q&A এর ৩টা প্রশ্নের উত্তর দিয়েছি এবং review পেয়েছি
- [ ] Tool টা চলে, অন্তত ৫টা real input এ test করেছি, result টেবিল আছে
- [ ] README তে লিখেছি: কী বানালাম, কেন, cost/latency, কোথায় ভুল করে
- [ ] Concept টা একজন non-technical founder কে ২ মিনিটে বোঝাতে পারবো

---

## Progress Tracker

| Module | বিষয় | Lessons | Status |
|---|---|---|---|
| 1 | GTM Fundamentals | 1.1 – 1.3 | 🟡 চলছে |
| 2 | ICP, Customer Research, Segmentation | 2.1 – 2.3 | ⬜ |
| 3 | SaaS Funnel ও Growth Metrics | 3.1 – 3.3 | ⬜ |
| 4 | Positioning ও Messaging | 4.1 – 4.3 | ⬜ |
| 5 | CRM ও Revenue Operations | 5.1 – 5.3 | ⬜ |
| 6 | Lead Generation ও Qualification | 6.1 – 6.3 | ⬜ |
| 7 | AI-Powered Sales Automation | 7.1 – 7.3 | ⬜ |
| 8 | AI Marketing Automation | 8.1 – 8.3 | ⬜ |
| 9 | AI Agents for GTM | 9.1 – 9.3 | ⬜ |
| 10 | Revenue Intelligence ও Analytics | 10.1 – 10.3 | ⬜ |
| 11 | Complete AI GTM Architecture | 11.1 – 11.3 | ⬜ |
| 12 | Enterprise Architecture ও Leadership | 12.1 – 12.3 | ⬜ |

**প্রতি ৩ module পর একটা Checkpoint Test** (scenario-based, founder call simulation সহ)।

---

## Module 1: GTM Fundamentals

**Module Objective:** GTM কী, কেন ভালো product ও fail করে, আর GTM team এ কে কী করে, সেটা পরিষ্কার বোঝা।
**Module Goal (শেষে পারবো):** যেকোনো SaaS এর website দেখে তার GTM strategy ব্যাখ্যা করতে পারবো।
**Flagship অংশ:** Company Research Agent এর ভিত্তি।

### Lesson 1.1: Go-To-Market আসলে কী? ✅ (শুরু হয়েছে)
- **Objective:** GTM এর ৫টা প্রশ্ন (কার জন্য, কেন, কোথায়, কীভাবে, কত দাম) বোঝা
- **গল্প:** করিম ভাই vs রহিমের চায়ের দোকান → রাফির AdGenie SaaS
- **Key terms:** ICP, Value proposition, Channel, Sales motion, Pricing, Repeatable
- **Tool পরিচিতি:** HubSpot, Apollo.io, Clay, n8n
- **Build: GTM X-Ray.** URL দিলে company এর GTM breakdown (LangGraph: fetch → extract → analyze → critic)
- **Branding:** LinkedIn headline update ("Building AI for Go-To-Market")
- **Done when:** X-Ray ৫টা SaaS এ চলেছে, evidence সহ output, cost/latency টেবিল
- **Detailed Build Prompt:** [`prompts/m1-l1-gtm-xray.md`](prompts/m1-l1-gtm-xray.md)

### Lesson 1.2: Sales Motion (PLG vs Sales-led vs Hybrid)
- **Objective:** Customer কীভাবে কেনে আর কোন product এ কোন motion মানায়, বোঝা
- **গল্প:** Canva (নিজে signup করে নিজে কেনে) vs Salesforce (৬ মাসের sales cycle, ১০ জনের meeting)
- **Key terms:** PLG, Sales-led, Hybrid, Self-serve, ACV (Annual Contract Value), Sales cycle, Free trial vs Freemium
- **Tool পরিচিতি:** Pricing page analysis (দাম দেখেই motion বোঝা)
- **Build: Pricing Page Analyzer.** X-Ray তে নতুন node: pricing page থেকে tier, price, "Contact Sales" button, free plan detect করে motion classify করা
- **Branding:** ৫টা কোম্পানির motion নিয়ে একটা ছোট carousel/post এর draft
- **Done when:** ১০টা company তে classification, নিজে হাতে যাচাই করা accuracy %

> **Build Prompt:** "Extend my existing LangGraph GTM X-Ray project with a `pricing_node`. It should find the pricing page (try /pricing, then search homepage links), extract tiers into a Pydantic model (name, price, billing period, is_free, has_contact_sales), and classify sales motion as PLG / Sales-led / Hybrid with a rule-based first pass and an LLM fallback only when rules are ambiguous. Log which path decided. Add tests with 3 saved HTML fixtures."

### Lesson 1.3: GTM Team ও Roles + GTM Engineer এর Job Market
- **Objective:** SDR, AE, CSM, Marketing, RevOps কে কী করে আর GTM Engineer কোথায় বসে, বোঝা
- **গল্প:** একটা lead এর জীবন: website visit থেকে signed contract, কার হাত ঘুরে যায়
- **Key terms:** SDR, BDR, AE, CSM, RevOps, Quota, Pipeline, Handoff
- **Tool পরিচিতি:** LinkedIn Jobs, Wellfound, RemoteOK এ "GTM Engineer" JD পড়া
- **Build: JD Gap Analyzer.** ২০টা remote GTM Engineer JD থেকে skill extract, frequency count, আর আমার profile এর সাথে gap report
- **Branding:** Gap report থেকে নিজের ৯০ দিনের learning goal public করা (optional)
- **Done when:** Top 10 required skill এর লিস্ট + আমার gap চিহ্নিত

> **Build Prompt:** "Build a Python CLI that takes a folder of job description text files, uses an LLM with structured output to extract {required_skills, nice_to_have, tools, seniority, salary_range, remote_policy}, normalizes skill names with embeddings-based dedupe, stores results in PostgreSQL, and prints a frequency table plus a gap analysis against a `my_profile.yaml`. Use a cheap model for extraction and cache results by file hash in Redis."

---

## Module 2: ICP, Customer Research ও Segmentation

**Module Objective:** "কার জন্য" প্রশ্নটার data-driven উত্তর দেওয়া শেখা।
**Module Goal:** একটা product এর জন্য machine-readable ICP বানিয়ে company গুলোকে match করতে পারবো।
**Flagship অংশ:** ICP Matching Agent।

### Lesson 2.1: ICP (Ideal Customer Profile) ও Firmographics
- **Objective:** ICP মানে কী, আর "সবাই আমাদের customer" কেন ভুল
- **গল্প:** এক startup ১০০ জন customer এর মধ্যে ১২ জন থেকে ৭০% revenue পায়; ঐ ১২ জনের মিল কোথায়?
- **Key terms:** ICP, Firmographics (size, industry, revenue, location), Technographics (কোন tool ব্যবহার করে), Buying signals, Disqualifier
- **Tool পরিচিতি:** Apollo/Clearbit এর filter দিয়ে ICP টানা
- **Build: ICP-as-Code.** YAML এ ICP define, Pydantic validator, আর company profile কে ICP এর সাথে match করে fit score + কারণ
- **Branding:** "Engineer হিসেবে ICP কে config file হিসেবে দেখি" এই angle এ post
- **Done when:** ২০টা company score করা, কেন match/mismatch তার explanation

> **Build Prompt:** "Create an `icp/` module: ICP definitions in YAML (must-have, nice-to-have, disqualifiers, weights), a Pydantic schema that validates them, and a `match(company_profile, icp) -> FitResult` function. Hard rules (employee range, geography, disqualifiers) are deterministic; fuzzy criteria (e.g. 'sells to SMBs') use an LLM judge that must cite evidence from the profile. Return score 0-100 and per-criterion reasons. Include pytest tests."

### Lesson 2.2: Buyer Persona, Jobs-to-be-Done ও Customer Interview
- **Objective:** Company না, **মানুষ** কেনে। কে কেনে, কে ব্যবহার করে, কে বাধা দেয়
- **গল্প:** CTO পছন্দ করলো, কিন্তু CFO দাম দেখে আটকে দিলো। deal মারা গেল
- **Key terms:** Persona, Economic buyer, Champion, End user, Blocker, JTBD, Pain point
- **Tool পরিচিতি:** G2/Capterra reviews, Reddit, customer interview script
- **Build: Review Pain Miner.** Public review গুলো থেকে pain point extract, embedding দিয়ে cluster, প্রতিটা cluster এর নাম আর উদাহরণ quote
- **Branding:** একটা category এর top pain cluster নিয়ে insight post
- **Done when:** ১টা category এর ২০০+ review থেকে ৫–৮টা pain cluster

> **Build Prompt:** "Build a pipeline that ingests product reviews (CSV: source, rating, text), extracts pain points and desired outcomes with structured output, embeds them, clusters with HDBSCAN, and asks an LLM to name each cluster and pick 3 representative quotes. Store in Postgres with pgvector. Expose `GET /clusters` via FastAPI. Report token cost per 100 reviews."

### Lesson 2.3: Segmentation ও Market Size (TAM/SAM/SOM)
- **Objective:** বাজারকে ভাগ করা আর কোন segment আগে ধরবো সেটা ঠিক করা
- **গল্প:** "Bangladesh এর সব দোকান" vs "ঢাকার ফার্মেসি যারা POS ব্যবহার করে"
- **Key terms:** Segment, Beachhead market, TAM, SAM, SOM, Bottom-up sizing
- **Build: Segment Explorer.** Company list কে firmographic + embedding feature দিয়ে segment করা, প্রতিটা segment এর size আর ICP fit গড়
- **Branding:** —
- **Done when:** ৩টা segment এর তুলনা আর কেন একটা beachhead বেছে নিলাম তার লিখিত যুক্তি

> **Build Prompt:** "Given a CSV of companies with firmographics and short descriptions, build a notebook + module that combines numeric features and description embeddings, clusters into segments, computes per-segment count, median size, and average ICP fit (reuse my `icp.match`), and produces a bottom-up TAM/SAM/SOM estimate with explicit, editable assumptions."

---

## Module 3: SaaS Funnel ও Growth Metrics

**Module Objective:** Founder এর ভাষা (CAC, LTV, MRR, NRR) বোঝা আর হিসাব করতে পারা।
**Module Goal:** যেকোনো feature/automation এর business impact সংখ্যায় দেখাতে পারবো।
**Flagship অংশ:** Revenue Analytics Dashboard এর data model।

### Lesson 3.1: Funnel: Lead থেকে Customer
- **Objective:** Lead → MQL → SQL → Opportunity → Closed Won, প্রতিটা ধাপের মানে
- **গল্প:** ১০০০ জন website এ এলো, ১ জন কিনলো। বাকি ৯৯৯ জন কোথায় হারালো?
- **Key terms:** TOFU/MOFU/BOFU, Lead, MQL, SQL, Opportunity, Win rate, Conversion rate, Velocity
- **Build: Funnel Event Store.** Postgres এ funnel event schema + stage-to-stage conversion আর time-in-stage SQL
- **Done when:** Synthetic data তে funnel report, কোথায় সবচেয়ে বেশি drop

> **Build Prompt:** "Design a PostgreSQL schema for GTM funnel events (lead_created, mql, sql, opp_created, closed_won, closed_lost) with lead/company/source dimensions. Write a synthetic data generator in Python with realistic drop-offs, and SQL views for stage conversion, median time-in-stage, and conversion by source. Add a FastAPI endpoint returning the funnel as JSON."

### Lesson 3.2: Unit Economics: CAC, LTV, Payback, Churn
- **Objective:** একজন customer আনতে কত খরচ আর সে কত দেয়, এটা না বুঝলে কোনো GTM কথা বলা যায় না
- **গল্প:** এক startup প্রতি customer আনতে $900 খরচ করে, customer দেয় $50/মাস, আর ১০ মাসে চলে যায়
- **Key terms:** CAC, LTV, LTV:CAC ratio, CAC payback, Churn, Gross margin, ARPU
- **Build: Unit Economics API.** Input দিলে CAC, LTV, payback, আর "AI SDR লাগালে কী বদলায়" scenario simulation
- **Branding:** "AI automation এর ROI কীভাবে হিসাব করি" ব্যাখ্যা post (hypothetical সংখ্যা স্পষ্ট করে বলে)
- **Done when:** ৩টা scenario এর তুলনা, নিজে founder কে বোঝাতে পারবো

> **Build Prompt:** "Build a FastAPI service with endpoints to compute CAC, LTV (with gross margin and churn), LTV:CAC, and CAC payback from input assumptions, plus a `/scenario` endpoint that compares baseline vs. 'AI-assisted outbound' assumptions (e.g. SDR hours saved, reply rate change) and returns the delta. Validate inputs with Pydantic and include unit tests with hand-calculated expected values."

### Lesson 3.3: MRR, NRR ও Cohort Analysis
- **Objective:** Recurring revenue কীভাবে বাড়ে/কমে আর cohort দিয়ে retention দেখা
- **গল্প:** MRR বাড়ছে, কিন্তু পুরনো customer রা চুপচাপ চলে যাচ্ছে
- **Key terms:** MRR, ARR, New/Expansion/Contraction/Churned MRR, NRR, GRR, Cohort
- **Build: MRR Movement + Cohort report.** Subscription data থেকে MRR bridge আর cohort retention table
- **Done when:** Cohort chart থেকে একটা insight লিখতে পারি

> **Build Prompt:** "From a subscriptions table (customer_id, plan, mrr, start_date, end_date, changes), compute monthly MRR movements (new, expansion, contraction, churn), NRR and GRR, and a monthly cohort retention matrix. Implement in SQL with a Python wrapper, and render a simple chart. Generate realistic synthetic data to test."

---

## Module 4: Positioning ও Messaging

**Module Objective:** Product কে কীভাবে describe করলে সঠিক customer বোঝে "এটা আমার জন্য"।
**Module Goal:** Feature-speak বাদ দিয়ে outcome-speak এ লিখতে আর AI-generated message evaluate করতে পারবো।
**Flagship অংশ:** Personalization Agent এর messaging layer।

### Lesson 4.1: Positioning
- **Objective:** Competitive alternative, unique value, target customer, category, এই উপাদানগুলো বোঝা
- **গল্প:** একই product "AI writing tool" বললে ১০০০ competitor, "Shopify store এর ad fatigue fix" বললে প্রায় কেউ না
- **Key terms:** Positioning, Competitive alternatives, Differentiation, Category, Value theme
- **Build: Competitor Positioning Map.** ৫টা competitor এর homepage থেকে claim extract আর comparison matrix
- **Done when:** একটা product এর positioning statement + competitor matrix

> **Build Prompt:** "Reuse my X-Ray fetcher to pull homepages of a product and its competitors. Extract claims (target customer, key outcomes, differentiators, proof points) into a structured schema, then build a comparison matrix and highlight 'white space' claims nobody makes. Output Markdown and JSON. Require source quotes for every claim."

### Lesson 4.2: Messaging Matrix (Persona অনুযায়ী বার্তা)
- **Objective:** CTO, CFO, Marketing Head, এদের জন্য একই product এর আলাদা গল্প
- **Key terms:** Messaging matrix, Value prop, Proof point, Objection
- **Build: Messaging Matrix Generator** with LLM-as-judge eval
- **Done when:** ৩ persona × ৩ value theme এর matrix, eval score সহ

> **Build Prompt:** "Build a generator that takes a positioning doc and a list of personas and produces a messaging matrix (persona × value theme → headline, pain, outcome, proof, objection-handling). Add an LLM-as-judge evaluator with an explicit rubric (specificity, outcome-focus, no unverifiable claims) and log scores per cell. Compare two prompt versions."

### Lesson 4.3: Cold Email এর মূলনীতি
- **Objective:** কেন ৯৯% cold email কেউ পড়ে না, আর ভালো email এর গঠন
- **গল্প:** "Hi {first_name}, I hope this email finds you well" vs একটা ৪ লাইনের specific email
- **Key terms:** Subject line, Hook, Relevance, CTA, Reply rate, Spam trigger
- **Build: Cold Email Grader.** Rubric-based grader + rewrite suggestion
- **Branding:** একটা খারাপ email কে ভালো বানানোর before/after post (নিজের লেখা উদাহরণ)
- **Done when:** ২০টা email grade করা, human judgment এর সাথে মিল %

> **Build Prompt:** "Create a cold email grader: rule-based checks (length, spam words, link count, personalization tokens left unfilled) plus an LLM rubric score (relevance, specificity, clear CTA). Return a score, issues list, and one rewrite. Build a small labeled set of 20 emails to measure agreement with my own grades."

---

## Module 5: CRM ও Revenue Operations

**Module Objective:** CRM এর data model আর RevOps এর কাজ বোঝা; AI এর output কোথায় জমা হবে।
**Module Goal:** HubSpot এর সাথে দুই দিকে sync করা production-grade integration বানাতে পারবো।
**Flagship অংশ:** CRM Integration।

### Lesson 5.1: CRM এর ভেতরে কী থাকে
- **Objective:** Contact, Company, Deal, Pipeline, Lifecycle stage, Activity
- **গল্প:** "বাকির খাতা" যখন ৫০ জন salesperson একসাথে লেখে
- **Key terms:** Object, Property, Association, Pipeline, Deal stage, Lifecycle stage, Owner
- **Tool পরিচিতি:** HubSpot free CRM, Private App token, API docs
- **Build: HubSpot Sync Client.** Python client: company/contact upsert, custom property তৈরি, rate limit handle
- **Done when:** X-Ray এর output HubSpot company record এ custom property হিসেবে বসে

> **Build Prompt:** "Build a typed Python HubSpot client (httpx, async) for companies, contacts, deals, and associations with upsert-by-domain/email, automatic retry with backoff on 429, Redis-based rate limiting, and creation of custom properties (e.g. `ai_icp_score`, `ai_research_summary`). Write an integration test against a HubSpot developer test account. Never hard-code tokens; read from env."

### Lesson 5.2: Data Hygiene, Dedupe ও Enrichment
- **Objective:** খারাপ data = খারাপ AI। Duplicate, পুরনো, ভুল data সামলানো
- **Key terms:** Enrichment, Dedupe, Data decay, Source of truth, Waterfall enrichment
- **Build: Enrichment Pipeline.** Multiple source থেকে waterfall enrichment + fuzzy dedupe
- **Done when:** ইচ্ছা করে নোংরা করা dataset পরিষ্কার করা, before/after metrics

> **Build Prompt:** "Build an enrichment pipeline with pluggable providers (start with a mock + my X-Ray), waterfall logic (try providers in order until fields are filled), per-field provenance and freshness timestamps, and a dedupe step using normalized domain + fuzzy name matching. Store in Postgres; emit a data quality report."

### Lesson 5.3: RevOps: Lead Routing, SLA ও Attribution
- **Objective:** সঠিক lead সঠিক মানুষের কাছে সঠিক সময়ে
- **Key terms:** Lead routing, Round robin, Territory, SLA, Speed-to-lead, Attribution (first/last/multi-touch)
- **Tool পরিচিতি:** n8n workflow, HubSpot webhook
- **Build: Lead Router.** HubSpot webhook → FastAPI → routing rules → owner assign → Slack notify (n8n)
- **Done when:** নতুন lead আসলে ১ মিনিটের মধ্যে assign আর notify

> **Build Prompt:** "Build a FastAPI webhook receiver for HubSpot contact/company creation events with signature verification, idempotency via Redis, and a rule engine (YAML) for routing by segment, ICP score, and territory. Assign owner via HubSpot API and trigger an n8n webhook for Slack notification. Include an n8n workflow JSON export."

---

## Module 6: Lead Generation ও Qualification

**Module Objective:** Lead কোথা থেকে আসে, আর কোন lead এ সময় দেওয়া উচিত।
**Module Goal:** Fit + intent মিলিয়ে explainable lead scoring system বানাতে পারবো।
**Flagship অংশ:** Lead Scoring Agent।

### Lesson 6.1: Inbound, Outbound ও Buying Signals
- **Objective:** কে "এখন" কিনতে পারে তার ইঙ্গিত চেনা
- **গল্প:** এক কোম্পানি একসাথে ৩ জন SDR নিয়োগ দিচ্ছে আর সদ্য Series A তুলেছে
- **Key terms:** Inbound, Outbound, Intent data, Trigger event, Signal-based selling
- **Build: Signal Collector.** Job post, funding news, website change থেকে signal detect
- **Done when:** ২০টা company র signal timeline

> **Build Prompt:** "Build a signal collector with pluggable sources (job postings page, news RSS, website diff over time). For each company, detect signal types (hiring for role X, funding, new product, leadership change) with structured output and evidence URL, deduplicate, and store as a timeline in Postgres. Schedule runs with a Redis-backed queue."

### Lesson 6.2: Qualification Frameworks (BANT, MEDDIC)
- **Objective:** Sales team কীভাবে ঠিক করে deal আসল নাকি সময় নষ্ট
- **Key terms:** BANT, MEDDIC/MEDDPICC, Discovery call, Champion, Decision process
- **Build: Call Transcript → MEDDIC Extractor**
- **Done when:** ৫টা (নিজে লেখা/public sample) transcript এ কোন field missing তা ধরতে পারে

> **Build Prompt:** "Build an extractor that takes a sales call transcript and fills a MEDDIC schema (metrics, economic buyer, decision criteria, decision process, identify pain, champion), each with quote evidence and confidence, plus a list of missing fields and suggested follow-up questions. Use chunking for long transcripts and a merge step in LangGraph."

### Lesson 6.3: Lead Scoring (Fit + Intent)
- **Objective:** Score মানে "কাকে আগে ফোন করবো"। Explainability জরুরি
- **Key terms:** Fit score, Intent score, Engagement score, Score decay, Threshold, Precision@K
- **Build: Hybrid Lead Scorer.** Rules + (পরে) ML + LLM reasoning, প্রতিটা score এর কারণ সহ
- **Branding:** "Black-box score কেন sales team বিশ্বাস করে না" post
- **Done when:** Score + reason HubSpot এ যায়, Precision@K হিসাব আছে (synthetic outcome দিয়ে)

> **Build Prompt:** "Build a lead scoring service combining ICP fit (from my icp module), intent signals (from signal collector, with time decay), and engagement events. Output total score, sub-scores, and top 3 human-readable reasons. Add an offline evaluation script computing precision@K against labeled outcomes, and push scores to HubSpot custom properties."

---

## Module 7: AI-Powered Sales Automation

**Module Objective:** Outreach কে personalize আর scale করা, কিন্তু spam না হয়ে।
**Module Goal:** Human approval সহ নিরাপদ AI outreach pipeline বানাতে পারবো।
**Flagship অংশ:** Personalization Agent + Human Approval Workflow।

### Lesson 7.1: Personalization at Scale ও Deliverability
- **Objective:** Real personalization vs fake ("I saw your LinkedIn"), আর email inbox এ না পৌঁছালে সব বৃথা
- **Key terms:** Personalization tier, Deliverability, SPF/DKIM/DMARC, Domain warmup, Bounce rate, CAN-SPAM/GDPR
- **Build: Personalization Agent.** Research + persona + messaging matrix থেকে email draft, guardrail সহ (কোনো unverifiable claim না)
- **Done when:** ১০টা draft, প্রতিটার personalization এর source cite করা

> **Build Prompt:** "Build a LangGraph personalization agent: inputs are company research, contact persona, and messaging matrix; nodes are angle_selection → draft → guardrail_check (no fabricated facts, every personal reference must map to a research evidence item, length limits) → grader (reuse my cold email grader). Retry up to 2 times on failure. Return draft + evidence map."

### Lesson 7.2: Sequences ও Multichannel Cadence
- **Objective:** একটা email না, ধাপে ধাপে follow-up (email, LinkedIn, call)
- **Key terms:** Sequence, Cadence, Step, Reply detection, Auto-pause, Opt-out
- **Build: Sequence Engine.** Redis-based scheduling, reply আসলে auto-stop
- **Done when:** Simulated ৫০ lead এ sequence চলে, reply/opt-out handle হয়

> **Build Prompt:** "Build a sequence engine: sequences defined in YAML (steps, delays, channels), enrollment API, Redis sorted-set scheduler, worker that renders step content (via personalization agent) and sends through a pluggable sender (mock first). Auto-pause on reply or opt-out events, enforce per-domain daily send limits, and keep a full audit log in Postgres."

### Lesson 7.3: Human-in-the-Loop Approval
- **Objective:** কখন AI নিজে পাঠাবে, কখন মানুষকে দেখাবে; trust কীভাবে তৈরি হয়
- **Key terms:** HITL, Approval queue, Confidence threshold, Edit tracking, Feedback loop
- **Build: Approval Workflow.** LangGraph interrupt + approval UI/Slack + edit গুলো থেকে শেখা
- **Branding:** Flagship engine এর প্রথম demo video (২ মিনিট)
- **Done when:** Draft → approve/edit/reject → send, আর edit rate dashboard

> **Build Prompt:** "Add human-in-the-loop to my outreach graph using LangGraph interrupts with a Postgres checkpointer. Expose approval endpoints (list pending, approve, edit, reject with reason), send a Slack message via n8n with approve/reject buttons, store original vs edited drafts, and compute edit distance and rejection reasons for a feedback report."

---

## Module 8: AI Marketing Automation

**Module Objective:** Marketing side এর automation (content, paid ads, nurture)। **এখানে আমার AdTech অভিজ্ঞতা সবচেয়ে বেশি কাজে লাগবে।**
**Module Goal:** Marketing এর কাজকে measurable pipeline এর সাথে যুক্ত করতে পারবো।

### Lesson 8.1: Content Engine ও SEO
- **Key terms:** SEO, Search intent, Keyword cluster, Content brief, Programmatic SEO
- **Build: SEO Content Brief Generator** (SERP analysis → brief, plagiarism/fact guardrail)

> **Build Prompt:** "Build a content brief generator: given a target keyword and ICP, fetch top-ranking pages (via a search API), extract headings and covered subtopics, find gaps, and output a structured brief (intent, outline, questions to answer, internal links, CTA tied to ICP pain). Cache fetches in Redis and cite sources."

### Lesson 8.2: Paid Ads ও Creative Testing
- **Key terms:** CPM, CPC, CTR, CPA, ROAS, Creative fatigue, Attribution window
- **Build: Creative Variant + Performance Analyzer** (ad performance data থেকে কোন angle কাজ করছে)
- **Branding:** নিজের AdTech অভিজ্ঞতা থেকে real শিক্ষা নিয়ে post (NDA মেনে, কোনো বানানো সংখ্যা না)

> **Build Prompt:** "Build an ad creative analyzer: ingest ad performance CSV (creative text, angle tags, spend, impressions, clicks, conversions), auto-tag angles with an LLM where missing, compute CTR/CPA/ROAS by angle with confidence intervals, detect creative fatigue over time, and generate new variants for the top angle with guardrails."

### Lesson 8.3: Lifecycle ও Nurture Email
- **Key terms:** Nurture, Lifecycle stage, Behavioral trigger, Activation, Re-engagement
- **Build: Behavior-based Nurture Segmenter**

> **Build Prompt:** "Build a nurture segmenter that reads product/engagement events, assigns users to lifecycle segments with explicit rules, picks the next best message from a library using an LLM ranker with reasons, and syncs segment membership to HubSpot lists."

---

## Module 9: AI Agents for GTM

**Module Objective:** আলাদা আলাদা tool কে নির্ভরযোগ্য multi-agent system এ জোড়া।
**Module Goal:** Production-ready, evaluated, cost-controlled GTM agent system design করতে পারবো।

### Lesson 9.1: GTM Agent Design ও MCP
- **Key terms:** Tool use, Agent memory, MCP (Model Context Protocol), Tool permission
- **Build: GTM MCP Server.** আমার tool গুলো (X-Ray, ICP match, scoring, HubSpot) MCP tool হিসেবে expose

> **Build Prompt:** "Wrap my existing GTM functions (xray, icp_match, score_lead, hubspot_upsert) as an MCP server with clear tool descriptions, input schemas, and read-only vs write permission flags. Write-tools must require a confirmation parameter. Add a demo client script."

### Lesson 9.2: Multi-Agent Orchestration
- **Key terms:** Supervisor pattern, Parallel fan-out, State, Checkpoint, Retry
- **Build: GTM Engine Orchestrator.** Research → ICP → Score → Personalize → Approve এক graph এ, batch processing সহ

> **Build Prompt:** "Compose my research, ICP matching, scoring, personalization, and approval nodes into a single LangGraph supervisor graph with parallel fan-out over a batch of companies, per-node timeouts and retries, Postgres checkpointing, and a run summary (processed, skipped by ICP, sent to approval, cost)."

### Lesson 9.3: Evals, Cost ও Reliability
- **Key terms:** Golden dataset, Regression eval, Cost per lead, Latency budget, Fallback model
- **Build: Eval Harness.** প্রতিটা agent এর golden set, CI তে eval চলে
- **Branding:** "GTM agent এর cost per qualified lead কীভাবে মাপি" technical blog

> **Build Prompt:** "Build an eval harness: golden datasets per component (JSONL), metric functions (exact match, rubric LLM-judge, evidence-faithfulness), a runner that reports quality, cost, and latency per component and model, and a GitHub Actions workflow that fails on regression beyond a threshold."

---

## Module 10: Revenue Intelligence ও Analytics

**Module Objective:** Data থেকে "কী হচ্ছে, কেন হচ্ছে, কী করা উচিত" বের করা।
**Module Goal:** AI system এর business impact honestly মাপতে আর দেখাতে পারবো।
**Flagship অংশ:** Revenue Analytics Dashboard।

### Lesson 10.1: Pipeline Analytics ও Forecasting
- **Key terms:** Pipeline coverage, Weighted pipeline, Forecast category, Deal slippage
- **Build: Pipeline Forecast** (stage-weighted + simple ML baseline)

> **Build Prompt:** "Build pipeline analytics over my funnel/deal tables: coverage ratio, weighted pipeline, slippage detection, and a forecast comparing stage-weighted vs. a gradient-boosting win-probability model, with backtesting on historical synthetic data."

### Lesson 10.2: Conversation Intelligence
- **Key terms:** Talk ratio, Objection, Competitor mention, Next step
- **Build: Call Analyzer** (MEDDIC extractor এর উপর dashboard)

> **Build Prompt:** "Extend my MEDDIC extractor into a call analyzer: talk ratio, objections, competitor mentions, next steps, risk flags per deal; aggregate across calls to show top objections and their win-rate impact."

### Lesson 10.3: Attribution ও Experiment Measurement
- **Key terms:** A/B test, Statistical significance, Holdout group, Incrementality, Multi-touch attribution
- **Build: Experiment Analyzer + Revenue Dashboard**
- **Done when:** "AI outreach vs manual" experiment এর design (holdout সহ) আর dashboard

> **Build Prompt:** "Build an experiment analyzer for outreach tests (variant assignment, reply/meeting/opportunity rates, significance tests, holdout comparison) and a dashboard (Streamlit or a simple React page via FastAPI) showing funnel, unit economics, agent cost, and experiment results."

---

## Module 11: Complete AI GTM Architecture

**Module Objective:** সব অংশ এক production architecture এ।
**Module Goal:** Flagship project শেষ, demo-ready, documented।

### Lesson 11.1: Reference Architecture
- Event-driven design, queue, idempotency, multi-tenant, observability
- **Build:** Architecture diagram + ADR (Architecture Decision Records)

### Lesson 11.2: Flagship Integration
- **Build:** Autonomous AI GTM Engine end-to-end: company list → research → ICP → score → personalize → approve → HubSpot → analytics

### Lesson 11.3: Demo ও Case Study
- **Build:** ৫ মিনিটের demo video, README, case study (honest metrics: synthetic/test data হলে সেটা স্পষ্ট লেখা)

> **Build Prompt (11.x):** "Review my repository as a staff engineer. Produce an architecture diagram (Mermaid), list gaps for production readiness (idempotency, retries, observability, secrets, multi-tenancy, PII handling), write ADRs for the 5 most important decisions, and create a docker-compose that runs FastAPI, workers, Postgres, Redis, and n8n together with seed data for a demo."

---

## Module 12: Enterprise Architecture ও Leadership

**Module Objective:** Founder/enterprise এর সাথে কথা বলা, compliance, আর career।
**Module Goal:** AI GTM Engineer interview আর founder discovery call আত্মবিশ্বাসের সাথে করতে পারবো।

### Lesson 12.1: Security, Compliance ও Data Governance
- GDPR, CAN-SPAM, PII, data retention, LLM data leakage, audit log
- **Build:** PII redaction layer + audit trail

### Lesson 12.2: Founder এর সাথে কথা বলা
- Discovery call, problem framing, proposal লেখা, scope/pricing নিজের service এর
- **Practice:** Mock founder call (আমি founder সাজবো)

### Lesson 12.3: Interview, Portfolio ও Job Hunt
- GTM Engineer JD decode, take-home assignment, system design interview (GTM version)
- **Practice:** Mock interview + portfolio review

> **Build Prompt (12.1):** "Add a PII governance layer to my GTM engine: detect and redact PII before LLM calls where not needed, field-level encryption for contact data at rest, retention policies with a cleanup job, unsubscribe/suppression list enforced across all senders, and an immutable audit log of every AI-generated outbound message."

---

## Self-Branding Track (পুরো course জুড়ে)

| সময় | কাজ |
|---|---|
| Module 1 | LinkedIn headline + About section আপডেট (সত্যি কথা: "learning/building") |
| Module 2–3 | প্রতি module এ ১টা "learning in public" post, real build result সহ |
| Module 4 | Portfolio site / GitHub profile README |
| Module 6–7 | Flagship demo video #1 |
| Module 8 | AdTech অভিজ্ঞতা থেকে insight post (NDA মেনে) |
| Module 9 | Technical blog: GTM agent cost/eval |
| Module 11 | পূর্ণ case study + demo |
| Module 12 | Job application, freelance/consulting offer |

**নিয়ম:** কোনো fabricated experience, client, বা revenue সংখ্যা না। Test/synthetic data হলে স্পষ্ট বলা।

---

## Flagship Project: Autonomous AI GTM Engine (Milestone Map)

```
 M1  ── Company Research Agent (X-Ray)
 M2  ── ICP Matching Agent
 M3  ── Funnel + Metrics data model
 M5  ── HubSpot integration + Lead routing (n8n)
 M6  ── Signal collector + Lead Scoring Agent
 M7  ── Personalization Agent + Sequence + Human Approval
 M9  ── Orchestrator + MCP + Evals
 M10 ── Revenue Analytics Dashboard
 M11 ── End-to-end, docker-compose, demo, case study
```
