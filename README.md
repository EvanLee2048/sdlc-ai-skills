# 🏛️ Automate the SDLC Paper Trail — From Discovery to UAT Sign-Off

### Four AI skills that turn the four deliverable-heavy phases of a consulting SDLC engagement — research, requirements, architecture, and UAT readiness — from days of drafting-and-review into one adversarially-tested run each. They don't write your code. They make sure everything that has to be approved *before* code gets written survives scrutiny the first time.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills](https://img.shields.io/badge/skills-4-blue)]()
[![SDLC Coverage](https://img.shields.io/badge/SDLC%20phases-discovery%20to%20UAT-purple)]()
[![Architecture](https://img.shields.io/badge/architecture-adversarial%20multi--agent-orange)]()
[![Gatekeepers](https://img.shields.io/badge/human%20gatekeepers-0%20mid--draft-red)]()

> A consulting SDLC engagement runs on four deliverables before a single line of code gets written: **research the problem, define the requirements, design the architecture, verify it's ready to test.** Each one normally costs days of senior time and at least one internal review cycle before it's fit to leave the building.
> **These four skills automate the drafting and the adversarial review behind each one — not the sign-off decision itself.** A human still decides what to do with a HIGH/MEDIUM/LOW output or a BLOCK verdict. What these skills remove is the two-day wait to find out your first draft wasn't good enough to make that decision on.

⭐ **Star this if you've ever burned two days on a first-draft BRD only to have it bounce back from review on page one.**

---

## Table of Contents

- [The Problem: Consulting Deliverables Are Slow Because Review Is Slow](#the-problem-consulting-deliverables-are-slow-because-review-is-slow)
- [Mapped to the Consulting SDLC](#mapped-to-the-consulting-sdlc)
- [The Fix: Automate the Draft-and-Attack Cycle, Not the Decision](#the-fix-automate-the-draft-and-attack-cycle-not-the-decision)
- [How the Pipelines Actually Work](#how-the-pipelines-actually-work)
- [The Four Skills](#the-four-skills)
- [Skill Comparison](#skill-comparison)
- [This vs. a Normal Prompt](#this-vs-a-normal-prompt)
- [Installation](#installation)
- [Usage](#usage)
- [Repository Structure](#repository-structure)
- [What You Actually Get](#what-you-actually-get)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## The Problem: Consulting Deliverables Are Slow Because Review Is Slow

Drafting a BRD, a TSD, a research memo, or a UAT sign-off recommendation isn't actually the bottleneck in a consulting engagement. **Getting it past review without two or three rounds of rework is.**

And when you draft it with a single AI pass, the review problem gets worse, not better — because the model reviewing your draft is the same model that wrote it. Nothing in that loop has any incentive, or any *ability*, to disagree with itself:

| What the engagement plan promised | What actually lands on the client's desk |
|---|---|
| "Independent market/technical research" | A confident memo with zero primary sources and a citation that doesn't resolve |
| "Requirements gathered from all stakeholders" | A BRD full of "the system should be user-friendly," with no acceptance criteria behind it |
| "Architecture reviewed for scalability" | A microservices diagram nobody asked for, no justification for why it wasn't just an existing service |
| "UAT plan validated and ready for sign-off" | A test plan with no numeric exit criteria, no independent validation method, and defect ownership nobody can name |

None of this is a talent problem. It's a **structural** one: self-review has no adversarial pressure. That's the review cycle you're actually paying for, every single deliverable, every single engagement — and it's the part that's automatable, even though the final sign-off shouldn't be.

---

## Mapped to the Consulting SDLC

These four skills aren't four random AI party tricks. They're built to sit exactly where the four core deliverables of an SDLC-based consulting engagement already sit — so you can drop one in per phase, or chain all four across a full engagement.

**Scope note:** this covers the four document-driven gates *before* build starts — Discovery, Requirements, Architecture, and UAT Readiness. It does not write, review, or deploy code. If your engagement also needs that covered, these four skills hand off cleanly into whatever dev/QA tooling you're already running.

| SDLC Phase | Engagement Deliverable | Skill | What Normally Slows This Down |
|---|---|---|---|
| **1. Discovery / Research** | Market, technical, or regulatory research memo | 🔬 `deep-research` | No fixed "right" experts to consult per topic — someone has to figure out the angles, then chase sources, then sanity-check claims |
| **2. Requirements** | BRD / FSD | 📋 `brd-fsd-design` | Vague requirements ("fast," "user-friendly") that don't survive a compliance or ops review, discovered only after the doc is "done" |
| **3. Design / Architecture** | Technical Spec Document | 🏗️ `tsd-design` | Over-engineered designs that don't map back to an actual requirement, caught (if at all) in a design review nobody budgeted time for |
| **4. Testing / UAT Readiness** | UAT plan review / sign-off recommendation | 🚨 `uat-plan-hostile-reviewer` | Test plans that look complete on paper but skip numeric exit criteria, independent validation, or defect ownership — caught only once testing has already started |

Chain them in order and you've automated the drafting-and-adversarial-review cycle for **Discovery → Requirements → Architecture → Test-Readiness Sign-Off** — the actual spine of most consulting SDLC engagements — with every handoff between phases passing through a hostile gate first, instead of only getting caught at the client review.

> You don't have to run all four. Plenty of engagements only need the BRD/FSD, or only need a hostile second opinion on a vendor's UAT plan. The point is that each skill is scoped to exactly one deliverable you already have to produce anyway — this isn't a new methodology to sell to your client, it's the one you're already running, just compressed from days to one run.

---

## The Fix: Automate the Draft-and-Attack Cycle, Not the Decision

Every skill here is built on the same belief:

> **The fastest way to ship a consulting deliverable that survives review is to automate a harsher review than the client will give it — before it ever leaves your machine.**

Three of these skills do that by **drafting under adversarial pressure**. The fourth does it by **auditing under adversarial assumption** — refusing to give an existing plan the benefit of the doubt. What none of them do is remove the human decision at the end. Here's how the mechanism plays out:

### 🧱 Personas Are Exiled, Not Roleplayed
*(applies to `deep-research`, `brd-fsd-design`, `tsd-design`)*
Every persona runs as its **own isolated sub-agent**, in its own tool session, with zero visibility into the others. Writing a persona's output inline instead of spawning a real, separate agent call is treated as a **critical failure** — the moment you fake isolation, three "perspectives" collapse back into one biased monologue, and you're back to a single-pass draft wearing a committee's confidence.

### ⚔️ A Hostile Reviewer, Not a Yes-Man
*(the one mechanism all four skills share)*
Every draft faces a **CRITIC** sub-agent explicitly instructed to attack it — factual errors, unsupported claims, contradictions, missing angles, over-engineering. The CRITIC is deliberately kept blind to how the draft was produced. No search history. No internal reasoning. Just the finished work, judged the way a skeptical client or a hostile stakeholder actually would.

`uat-plan-hostile-reviewer` makes this the *entire* skill instead of one phase of it: there's no drafting step to be hostile *after* — it opens hostile, on a document it's never seen, assuming it's broken until the evidence says otherwise.

### 🚫 Zero Human Babysitting Mid-Draft
This is the specific thing being automated — not the final call, the *iteration loop* that used to require a human to notice something was wrong and ask for a redo:
- CRITIC rejects it → automatically re-dispatched to the exact persona with exact feedback
- A submitted plan is missing a control → flagged as a cited finding with a required fix, never assumed present
- Can't find a source → flagged as an honest "data gap," never invented
- A sub-agent times out → retried with reduced scope, not abandoned

### 🔲 Overlap Gets Hunted Down, Not Ignored
*(applies to `deep-research`, `brd-fsd-design`, `tsd-design`)*
A structured 5-signal test — **Mechanism, Evidence, Problem, Benefit, Outcome** — runs across every section pair, across every persona, catching the double-counted benefits and contradictory recommendations that otherwise surface for the first time in the client meeting.

### 🎯 Confidence Is Earned, Never Assumed — and Never Automated Away
Every drafting run ships an honest **HIGH / MEDIUM / LOW** confidence tag, based on how many fights the CRITIC actually won. `uat-plan-hostile-reviewer` ships a **BLOCK / CONDITIONAL PASS / PASS** verdict, based on how many Critical findings survived the scan. Neither one auto-approves itself. The tag or verdict is the automated part; deciding what to do about a LOW-confidence memo or a BLOCK verdict is still yours.

### 📎 Nothing Is Allowed to Be Orphaned
Every claim traces to a citation. Every business requirement traces to a functional requirement, to an acceptance criterion, to a test case. Every red-flag finding traces to the exact clause in the submitted plan — or an explicit "NOT FOUND IN DOCUMENT." A broken link anywhere in that chain is a rejected draft or a blocked plan, not a footnote a human has to catch later.

---

## How the Pipelines Actually Work

There are **two distinct architectures** in this repo, matching the two kinds of consulting work above: producing a new deliverable, and auditing one you were handed.

### Architecture 1 — Draft, Attack, Repeat
*(`deep-research`, `brd-fsd-design`, `tsd-design`)*

Phase 1 — STORM Planning (in-context)
→ Lock the outline / fixed Table of Contents
→ Cast 3 personas, each with a distinct, non-overlapping lens
│
Phase 2 — Parallel Isolated Execution (3× independent sub-agents)
→ Persona A drafts   │   Persona B drafts   │   Persona C drafts
→ Each one gets its OWN tools, OWN context — no peeking
│
▼
Phase 3 — The Hostile CRITIC (1× isolated sub-agent, blind review)
→ Attacks the combined drafts: facts, logic, overlap, gaps
→ Verdict: APPROVED  or  REJECTED (+ exact fixes required)
│
┌───────────────┴───────────────┐
▼                               ▼
APPROVED                        REJECTED
│                               │
│                    Phase 4 — The Rematch
│                    → Rejected personas get a fresh shot
│                    → CRITIC's feedback injected as ammo
│                    → Back to Phase 3 (max 3 rounds)
│                               │
└───────────────┬───────────────┘
▼
Phase 5 — Synthesis (in-context)
→ One final document, honestly labeled
→ Confidence: HIGH / MEDIUM / LOW
→ CRITIC's sign-off + unified sources
→ Human decides what happens next


vbnet

**The one rule that can't be broken:** every persona and every review is its own tool call. Simulate a persona inline instead of actually spawning it, and the whole quality guarantee evaporates.

### Architecture 2 — Classify, Then Attack What's Already There
*(`uat-plan-hostile-reviewer`)*

Input — An existing plan/document (yours, a vendor's, a client's)
│
▼
Phase 1 — Domain Applicability Pre-Check (in-context)
→ Classify: Harmful-adjacent? Regulated-content? Multilingual?
Human-escalation-capable?
→ Conditional rules only activate where a flag is actually TRUE
→ Prevents false-positive Critical findings on unrelated plans
│
▼
Phase 2 — Lifecycle-Wide Red-Flag Scan (in-context)
→ Scoping → Design → Sandbox → UAT Entry → Methodology →
Validation → Execution/Governance → Exit Criteria
→ Every item scored PRESENT / PARTIAL / MISSING / N-A
→ Every finding cites the exact clause, or states NOT FOUND
│
▼
Phase 3 — Verdict
→ 2+ Critical findings → mandatory BLOCK, no exceptions
→ Otherwise → CONDITIONAL PASS or PASS + prioritized fix list
→ Human decides what to do with the verdict


vbnet

**The one rule that can't be broken here:** the Domain Pre-Check always runs *before* any conditional rule is scored — otherwise you're automating a "hostile review" that's hostile about the wrong things.

---

## The Four Skills

One is a generalist researcher. Two are drafting specialists. One doesn't draft at all — it audits. Know which SDLC phase you're in before you reach for one:

| Skill | SDLC Phase | What It Produces | Who's in the Room | Reach for This When |
|---|---|---|---|---|
| 🔬 [`deep-research`](./skills/deep_research.md) | Discovery | Multi-perspective research report on **any topic** | 3 experts, **auto-cast by the AI itself** based on what the topic needs | Kicking off an engagement and you need real research on a market, technology, or regulation before scoping starts |
| 📋 [`brd-fsd-design`](./skills/brd-fsd-design.md) | Requirements | BRD/FSD (23-section fixed structure) | Stakeholder · Compliance · Operator — **always these three** | You're tired of requirements docs full of "the system should be user-friendly" bouncing back from review |
| 🏗️ [`tsd-design`](./skills/tsd-design.md) | Design / Architecture | Technical Spec Document (24-section fixed structure) | Stakeholder · Compliance · Technical Architect — **always these three** | You have a BRD/FSD and need architecture that doesn't reinvent Kubernetes for a to-do app |
| 🚨 [`uat-plan-hostile-reviewer`](./skills/uat-plan-hostile-reviewer.md) | Testing / UAT | A BLOCK / CONDITIONAL PASS / PASS verdict on **a plan you already have** | Nobody drafts — one hostile auditor scans, cites, and refuses to assume good faith | A vendor, partner, or past engagement handed you a UAT plan or test strategy, and you need to know what's missing before you recommend sign-off |

> Chain all four and you've automated the drafting-and-review cycle for a full pre-build engagement: `deep-research` → `brd-fsd-design` → `tsd-design` → `uat-plan-hostile-reviewer`. Discovery to test-readiness, with an adversarial gate at every handoff — including the last one, right before UAT actually starts. None of the four decide anything on your behalf; they just make sure what reaches you is already fit to decide on.

### 🔬 Deep Research — General-Purpose, Self-Casting
There's no fixed "Stakeholder/Compliance/Operator" cast here, because a discovery-phase research topic doesn't have universal roles the way a requirements doc does. Instead, the pipeline's own **STORM planning phase reads the topic first and invents the right three experts for it** — a crypto research question gets a different cast than a supply-chain question, which gets a different cast again than a regulatory question. Each self-identified persona then goes off in total isolation to do real, independent research — and a hostile CRITIC still tears the combined draft apart looking for factual errors, redundant sections, and claims that don't survive a source check. Includes hardened rules for jurisdictional/regulatory claims: no persona gets to *assume* a rule — they have to find it.

### 📋 BRD/FSD Design — Fixed Roles, Fixed Structure
Unlike `deep-research`, the cast here is locked: Stakeholder, Compliance, Operator, every time. Requirements docs don't need a novel cast per engagement — they need the same three lenses applied with merciless discipline. A locked 23-section structure and unforgiving requirement hygiene: every requirement gets a unique ID, has to describe exactly one behavior, and gets rejected outright if it says "fast" or "user-friendly" without a number attached. Every business requirement has to prove it leads somewhere — to a functional requirement, to a testable acceptance criterion.

### 🏗️ TSD Design — Fixed Roles, Fixed Structure
Same logic as `brd-fsd-design`: Stakeholder, Compliance, Technical Architect, always. Takes an approved BRD/FSD and turns it into a real architecture — with two extra weapons the CRITIC uses:
- **The Build-vs-Reuse Ladder** — the Technical Architect has to justify, every single time, why they're building something new instead of reusing what already exists.
- **The Over-Engineering Audit** — the CRITIC actively hunts for unjustified microservices and abstraction layers nobody's requirement asked for. The one thing it will never let you cut for simplicity: security controls.

### 🚨 UAT Plan Hostile Reviewer — No Drafting, No Cast, No Mercy
This is the outlier, deliberately. It never writes a plan — it only reads one, cold, the way an external auditor or an incoming program director would: **assume every unaddressed risk is a live risk, not an oversight.** It walks the entire project lifecycle — scoping, requirements/design, sandbox, UAT entry, test methodology, result validation, execution governance, and exit criteria — and scores every phase against a fixed red-flag registry built from real, hard-won AI-project failure patterns (unbudgeted testing costs, same-model validation bias, sandbox environments that don't match production, exit criteria nobody quantified). Its one piece of internal discipline the drafting skills don't need: a **Domain Applicability Pre-Check**, run before anything else, so it never penalizes an unrelated AI project for lacking harmful-routing logic it was never supposed to have. Two or more Critical findings, and it blocks — no diplomatic hedging, and no auto-override of that block, ever.

---

## Skill Comparison

| Dimension | `deep-research` | `brd-fsd-design` | `tsd-design` | `uat-plan-hostile-reviewer` |
|---|:---:|:---:|:---:|:---:|
| SDLC Phase | Discovery | Requirements | Design / Architecture | Testing / UAT |
| Job type | **Drafts** original research | **Drafts** an original document | **Drafts** an original document | **Audits** a document someone else already wrote |
| Cast of personas | 🎭 **Self-identified per topic** by STORM planning | 🔒 Fixed: Stakeholder/Compliance/Operator | 🔒 Fixed: Stakeholder/Compliance/Tech Architect | ❌ None — single hostile auditor |
| Structure | 🎨 Custom outline, designed per topic | 🔒 Fixed 23 sections | 🔒 Fixed 24 sections | 🔒 Fixed 8-phase lifecycle *review checklist* |
| Hostile CRITIC | ✅ (final gate) | ✅ (final gate) | ✅ (final gate) + over-engineering audit | ✅ (the entire skill) |
| MECE overlap check | ✅ | ✅ | ✅ | ➖ N/A — see Domain Pre-Check instead |
| Domain Applicability Pre-Check | ➖ N/A | ➖ N/A | ➖ N/A | ✅ **Required first step** |
| Traceability | Citations | BR → FR → AC | BR → FR → NFR → Component → Test | Every finding cites the input's exact clause, or flags NOT FOUND |
| Confidence signal | HIGH/MEDIUM/LOW | HIGH/MEDIUM/LOW | HIGH/MEDIUM/LOW | BLOCK / CONDITIONAL PASS / PASS |
| Max rematches | 3 | 3 | 3 | ➖ N/A — fix and re-submit |
| Final decision maker | You | You | You | You |
| Needs input first | Just a topic | Business context | Approved BRD/FSD and/or NFRs | An existing plan/document to point it at |

> **Why the difference?** The three drafting skills all *create* something new, so they all need the same defense against a single voice quietly agreeing with itself: isolate the drafters, then attack the draft. `uat-plan-hostile-reviewer` never creates anything — there's no draft to isolate, so a persona cast and a rematch loop would be theater bolted onto a job that doesn't need it. Its safeguard is different by design: a Domain Applicability Pre-Check, which stops the one failure mode an audit-only skill is actually at risk of — being hostile about the *wrong* things. Note the row every skill agrees on: **you** are always the final decision maker. Automation stops at the verdict.

---

## This vs. a Normal Prompt

| | "Act as three experts" prompt | "Review this carefully" prompt | This Repo |
|---|---|---|---|
| Speed to a review-ready draft | Fast to produce, slow to survive review | N/A | Fast to produce *and* pre-survives the review that used to take days |
| Perspectives | Same context, same biases, different fonts | N/A | Physically separate agents, separate tools, zero shared memory (drafting skills) |
| Review | The writer marks its own homework | The writer marks its own homework, again | A blind, hostile third party — including a dedicated skill that does *only* this |
| Missing sources / controls | Shipped anyway, confidently | Assumed present unless obviously absent | Flagged as a "data gap" or "MISSING," never faked |
| False positives on irrelevant risks | N/A | Common — generic checklists flag things that don't apply | Domain Applicability Pre-Check scopes conditional rules before they fire |
| Structure | Whatever mood the model's in | Whatever the reviewer remembers to check | Locked, enforced, no drift (or intentionally custom for `deep-research`) |
| Confidence / Verdict | Implied by tone | Implied by tone | Explicit, earned, honest when it's low or when it blocks |
| Who signs off | Unclear — everything reads "done" | Unclear | Always you — the skill hands you a decision-ready output, not a decision |

---

## Installation

Each skill is a self-contained Markdown definition (YAML frontmatter + instructions), built for any agent runtime with sub-agent delegation and `web` / `terminal` / `file` toolsets. `uat-plan-hostile-reviewer` needs less — it just needs to read the document you point it at.

```bash
git clone https://github.com/<your-username>/<your-repo>.git

# Drop the ones you want into your agent's skills directory
cp skills/deep_research.md               ~/.your-agent/skills/deep-research/SKILL.md
cp skills/brd-fsd-design.md               ~/.your-agent/skills/brd-fsd-design/SKILL.md
cp skills/tsd-design.md                   ~/.your-agent/skills/tsd-design/SKILL.md
cp skills/uat-plan-hostile-reviewer.md    ~/.your-agent/skills/uat-plan-hostile-reviewer/SKILL.md
Built for Claude Agent Skills–style manifests and any orchestrator that exposes a delegate_task(goal, context, toolsets) primitive. uat-plan-hostile-reviewer doesn't require sub-agent delegation to function, but runs fine inside the same orchestrator as the other three.

Usage
No special syntax. Just describe what you need — each skill activates on natural-language triggers, and each one maps to a phase of the engagement.

Discovery (deep-research — the AI casts its own experts)


css
"Do a deep-research report comparing stablecoin settlement options for cross-border payroll."
Requirements (brd-fsd-design — fixed Stakeholder/Compliance/Operator cast)


css
"I need a BRD/FSD for an automated invoice reconciliation system."
Design / Architecture (tsd-design — feed it the output of brd-fsd-design)


python
"Here's the approved BRD/FSD [attached]. Generate the TSD / technical architecture document."
Testing / UAT Readiness (uat-plan-hostile-reviewer — audit a plan you already have)


css
"Here's our vendor's UAT plan for a new AI chatbot [attached]. Run a hostile review —
tell me if it's actually ready, and cite exactly what's missing."
Every drafting run produces one finished Markdown document — executive summary, CRITIC's sign-off, honest confidence tag, unified references. uat-plan-hostile-reviewer produces one verdict report — Domain Pre-Check results, phase-by-phase coverage map, cited findings, and a plain-language recommendation. Either way, what you get is something ready for your decision, not a decision already made for you.

Repository Structure

bash
.
├── skills/deep_research.md                # Skill: Discovery-phase, self-casting research pipeline
├── skills/brd-fsd-design.md               # Skill: Requirements-phase BRD/FSD pipeline
├── skills/tsd-design.md                   # Skill: Design-phase Technical Spec pipeline (consumes BRD/FSD)
├── skills/uat-plan-hostile-reviewer.md    # Skill: Testing-phase, domain-aware hostile audit of UAT/project plans
└── README.md
What You Actually Get
Every deliverable these skills produce comes with receipts — the kind an engagement lead can hand to a client without a re-check, and the kind that make clear where automation stops and your judgment starts:

✅ A CRITIC Sign-Off — a paper trail of exactly what got attacked and what got fixed (drafting skills)
✅ A verdict with citations — every red-flag finding points at the exact clause in your plan, or states plainly that it's missing (uat-plan-hostile-reviewer)
✅ An honest confidence tag or BLOCK/CONDITIONAL PASS/PASS verdict — never an auto-approval
✅ Inline citations on every non-obvious claim, primary sources preferred
✅ "Data gap" / "MISSING" flags instead of fabricated facts or assumed compliance
✅ A Domain Applicability Pre-Check that keeps the audit honest about which risks actually apply to your project
✅ Full traceability from requirement → build → test (brd-fsd-design / tsd-design)
✅ A clear stopping point — every output ends with "here's what this is, here's how sure it is," and hands the actual decision to you
FAQ
"Is this a new methodology I have to sell to my client?"
No — it's the same four deliverables most SDLC-based consulting engagements already produce (research, BRD/FSD, TSD, UAT sign-off). This just automates how long each one takes to reach review-ready, and pre-survives the review cycle that usually eats the schedule.

"Does 'automate' mean this replaces my judgment on the deliverable?"
No. What's automated is the drafting-and-adversarial-review cycle — the multi-day loop of draft, get reviewed, get told what's wrong, redraft. What's never automated is the decision to accept, reject, or act on the output. A HIGH-confidence research memo still needs you to decide what it means for the engagement. A BLOCK verdict on a UAT plan still needs you to decide how to raise it with the client.

"Does this cover the whole SDLC, including build and deployment?"
No, and this is intentional, not a limitation to hide. It covers the four document-driven gates before build starts: Discovery, Requirements, Architecture, and UAT Readiness. It doesn't write, review, or deploy code. If your engagement also needs that covered, these four skills hand off cleanly into whatever dev/QA tooling you're already running.

"Can't I just tell the model to review its own work carefully?"
You can ask. It won't disagree with itself. Self-review has zero adversarial pressure — it's the same context grading its own exam and giving itself full marks. That's the exact failure this repo exists to kill.

"Why not just prompt 'act as three experts'?"
Because roleplaying shares one context, one memory, one set of biases. Three "perspectives" from the same context quietly converge into one voice within a few paragraphs. Real isolation — separate sub-agents, separate tool sessions — is the only way to guarantee they actually disagree when they should.

"Why does deep-research invent its own personas while the other drafting skills don't?"
Because requirements and architecture are closed domains — every engagement benefits from the same Stakeholder/Compliance/Operator (or Technical Architect) lenses, so locking them removes guesswork. Discovery-phase research is an open domain — the right experts for a legal question aren't the right experts for a market-sizing question. So deep-research's planning phase looks at your specific topic first and designs the cast before any research begins.

"Why doesn't uat-plan-hostile-reviewer use three personas and a rematch loop like the others?"
Because it isn't drafting anything. A persona cast exists to generate multiple independent drafts that can then disagree with each other — there's no draft here, just an existing document being read cold. Its safeguard against sloppy review is different: a mandatory Domain Applicability Pre-Check, which stops it from manufacturing Critical findings about risks that were never applicable to the plan in front of it.

"Can I chain all four across one engagement?"
Yes — that's the intended use. deep-research for discovery, brd-fsd-design for requirements, tsd-design for architecture, uat-plan-hostile-reviewer before UAT starts. Draft under adversarial pressure at each phase, then audit the resulting test strategy under adversarial assumption before a single tester runs a single test case.

"What if the CRITIC never approves?" (drafting skills)
It gets 3 rounds to make its case. After that, the pipeline ships anyway — clearly labeled LOW confidence, with every unresolved objection listed in plain sight. It never auto-escalates itself to "approved."

"What if uat-plan-hostile-reviewer blocks my plan and I don't agree?"
Every Critical and High finding cites the exact evidence that triggered it. Fix the plan, or document why a finding doesn't apply, and re-submit for a fresh scan. The BLOCK is a recommendation with receipts, not an unappealable veto.

"Can I run tsd-design on its own?"
It expects an approved BRD/FSD and/or NFR document going in. Run brd-fsd-design first if you don't have one yet.

Contributing
Issues and PRs welcome — especially:

New domain-specific tuning for deep-research's persona-casting logic
New fixed-structure variants (PRD, RFC, etc.) built on the drafting pipeline
Sharper MECE / over-engineering detection heuristics
New red-flag categories or Domain Pre-Check flags for uat-plan-hostile-reviewer
Real-world failure reports (timeouts, weird routing-loop edge cases, or plans that slipped past the reviewer)
Open an issue describing the failure before submitting big structural PRs — the rigidity is intentional, so changes should extend the pipeline, not loosen it.

License
MIT License — Fork it, ship it, put it to work in your own engagements.

<div align="center">
Automate the paper trail. Keep the judgment yours.
⭐ Star this repo — it's the fastest way to help the next person compress their SDLC engagement without cutting the rigor that makes it defensible.

</div> ```