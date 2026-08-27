# Makan Traore

IT student (Cloud Engineering) at **Asia Pacific University**, Kuala Lumpur. I build and ship products — mostly TypeScript, Node and cloud.

**Seeking a 16-week software engineering internship: 4 January – 23 April 2027, on-site in Malaysia.**

---

### What I've built

**[Venlio](https://getvenlio.com)** — *Multi-tenant SaaS, in production*
An AI sales assistant that e-commerce merchants embed on their store with a single script tag. Hono + TypeScript on Google Cloud Run, Firestore, Gemini via Vertex AI, and a ~15 KB vanilla-JS widget isolated in a Shadow DOM. Signature-verified billing webhooks, atomic monthly quota enforcement, per-tenant CORS allowlisting, and SSRF-guarded catalogue import from Shopify and WooCommerce.
Solo founder and developer. Architecture, security decisions, production debugging and deploys are mine.

**[CivicBridge AI](https://github.com/traoremakan483-prog/civicbridge-ai)** — *Multilingual RAG — built in a 2-day hackathon, rebuilt since*
A public-service navigator answering in eight languages, grounded in a curated knowledge base, showing the exact source excerpts it used alongside a plain-language explanation and concrete action steps.
The part I would point at: the threshold that decides whether it answers or refuses was a number nobody had measured. Scored against the real guides, it was **refusing half the legitimate questions** — *Does it cover an ambulance?*, *Where do I submit the form?* — all answered by the documents. `scripts/eval_retrieval.py` now scores forty questions and prints both distributions; the threshold sits in the gap between them, and 40 of 40 classify correctly. LangChain's own relevance scores turned out to go negative, so the conversion is done in one named, tested function instead.

**[NetCraft AI](https://netcraft-ai.vercel.app)** — *Network design SaaS*
Describe your sites, departments and devices; it generates the VLSM addressing plan, VLAN assignment and per-device Cisco IOS configuration, then validates the whole design against 16 best-practice rules. Next.js 16, Prisma, PostgreSQL.

**[AWS Home Lab](https://github.com/traoremakan483-prog/aws-home-lab)** — *Hands-on cloud infrastructure*
A full AWS environment built end-to-end in `ap-southeast-1`: custom VPC with public and private subnets, EC2 running Apache, an S3 static site, a private RDS MySQL instance reachable only from the web tier's security group, and a dedicated IAM identity. Console and CLI, no abstractions — documented service by service.

---

### How I work

I use AI coding agents — Claude Code, Cursor — as my main implementation tool. I define the problem, choose the architecture, write the requirements, and review what comes back. I debug production issues from logs myself, and I do all the deploys.

A concrete example: Venlio's generated demo links were silently failing — the API returned `200` but the store never rendered. I traced it through Cloud Run logs to Firestore rejecting `undefined` field values, which meant any catalogue containing a product without an image failed to persist without raising. I fixed the write path, made the endpoint fail loudly, and added a QA rule: never send a demo link without fetching it first.

What I care about most is how a thing is confirmed to work. On the clinic platform, the records are children's medical files, so I moved the application onto a non-privileged database role and wrote a **27-test suite** proving that a query bypassing the access layer returns no rows, that one family cannot read another's records, and that a payment cannot be altered even by the database owner. Switching that role surfaced six places where access control had never actually applied — all invisible while the app ran as the table owner. Then I disabled one rule on purpose to confirm the tests would fail: a test that cannot fail proves nothing.

---

### Currently

**TypeScript · Node.js · Next.js · Python · PostgreSQL · Firestore · Google Cloud Run · Vertex AI · OpenAI · FAISS · AWS · Terraform · Docker · Java · Cisco networking**

Learning in the open: raw SQL, Linux internals, and collaborative Git workflows.

📍 Kuala Lumpur · 🇫🇷 French (native) · 🇬🇧 English (professional)
