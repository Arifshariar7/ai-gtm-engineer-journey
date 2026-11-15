# Build Prompt: GTM X-Ray (Module 1, Lesson 1)

## কীভাবে ব্যবহার করবো
1. একটা নতুন খালি folder খুলে Claude Code (বা অন্য AI coding tool) চালু করো।
2. নিচের "Prompt" অংশটা পুরোটা copy করে দাও।
3. AI প্রথমে plan দেখাবে। **Plan টা নিজে review করো**, দরকার হলে বদলাও, তারপর build করতে দাও।
4. Build শেষে নিজে ৫টা company তে চালাও আর result টেবিল নিজে পূরণ করো। এই অংশ AI কে দিয়ে করাবে না, কারণ এখানেই শেখা।

> উদ্দেশ্য: AI দিয়ে boilerplate দ্রুত লেখানো। Architecture, eval আর "AI কোথায় ভুল করছে" বোঝা তোমার কাজ।

---

## Prompt

```text
You are helping me build "GTM X-Ray", the first component of a larger
Autonomous AI GTM Engine. I am a senior AI/backend engineer, so write
production-quality code, but keep the scope small and explain key decisions.

## Goal
Given a company website URL, produce a structured Go-To-Market breakdown:
who they sell to (ICP), the core pain they solve, likely acquisition channels,
sales motion (PLG / Sales-led / Hybrid), and pricing model. Every claim must
be backed by evidence quoted from the fetched pages.

## Stack
- Python 3.12, uv for dependency management
- FastAPI (API), LangGraph (orchestration), Pydantic v2 (schemas)
- httpx (async fetching), selectolax or BeautifulSoup (HTML -> text)
- Redis (page cache + simple rate limit)
- PostgreSQL (store runs and results) via SQLAlchemy 2.0 async
- An LLM provider abstraction so I can switch models via env vars;
  default to a small/cheap model for extraction and a stronger model for analysis
- docker-compose for Postgres + Redis
- pytest

## LangGraph design
State: url, pages: dict[path, text], facts, breakdown, critique, metrics.

Nodes:
1. fetch_node
   - Fetch homepage, then try /pricing, /customers, /about, /product
     (and links on the homepage whose text matches those words).
   - Convert HTML to clean text, cap each page at ~6k tokens.
   - Cache by URL in Redis (TTL 24h). Respect robots.txt. Timeout 10s per page.
2. extract_node (cheap model)
   - Turn raw page text into a list of atomic facts:
     {fact, source_path, quote}. No interpretation here.
3. analyze_node (strong model)
   - From facts only, produce GTMBreakdown (schema below).
   - Must not use outside knowledge about the company; only the facts.
4. critic_node
   - Check that every field in GTMBreakdown maps to at least one quote.
   - Unsupported fields -> mark as "unknown" and lower confidence.
   - Output critique notes and a final confidence 0-1.

## Output schema
class GTMBreakdown(BaseModel):
    company: str
    icp: str
    core_pain: str
    likely_channels: list[str]
    sales_motion: Literal["PLG", "Sales-led", "Hybrid", "unknown"]
    pricing_model: str
    evidence: dict[str, list[str]]   # field name -> supporting quotes
    confidence: float
    critique: list[str]

## Metrics (important)
For each run, record per node: model used, input tokens, output tokens,
estimated cost in USD (prices from a config file I can edit), latency ms.
Store the run, metrics, and result in Postgres.

## API
- POST /xray {url} -> GTMBreakdown + run_id + metrics
- GET /runs/{run_id}
- GET /runs?limit=20

## CLI
- `python -m xray batch companies.txt` runs a list of URLs and writes
  results.md with a table: company | ICP | motion | pricing | confidence |
  cost | latency, plus an empty "My verdict (correct/wrong/why)" column
  for me to fill by hand.

## Quality
- Type hints everywhere, ruff + mypy clean.
- Tests: unit tests for HTML cleaning and critic logic using saved HTML
  fixtures (no network in tests); one LLM call mocked end-to-end test.
- Secrets only from .env (provide .env.example). Never commit .env.
- README: architecture diagram (Mermaid), setup, how to run, cost notes,
  known limitations.

## How to work with me
1. First, show me the project structure and a short plan. Wait for my OK.
2. Then build in small steps: schemas -> fetch -> extract -> analyze ->
   critic -> API -> CLI -> tests. Run tests after each step.
3. Do not invent example results or metrics in the README. Leave a
   "Results" section for me to fill after I run it.
```

---

## Build শেষে নিজের Checklist
- [ ] ৫টা company তে চালিয়েছি (Notion, HubSpot, Canva, Linear, + ১টা নিজের পছন্দের)
- [ ] `results.md` এর "My verdict" column নিজে পূরণ করেছি
- [ ] কোন field এ AI সবচেয়ে বেশি ভুল করে, কেন, ২–৩ লাইনে লিখেছি
- [ ] প্রতি run এর গড় cost আর latency জানি
- [ ] Extract এ ছোট model আর analyze এ বড় model দিলে cost/quality কেমন বদলায়, একবার তুলনা করেছি

## Stretch (ঐচ্ছিক)
- Small vs large model দিয়ে পুরো run এর quality/cost তুলনার টেবিল
- Lesson 1.2 এর `pricing_node` আগেই যোগ করা
