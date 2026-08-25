# 🏛️ Stop Letting Your AI Grade Its Own Homework

### Three battle-tested agent skills that turn one overconfident AI voice into a research team, a compliance officer, and a hostile reviewer — so what lands in your inbox has already survived a fight before you ever see it.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills](https://img.shields.io/badge/skills-3-blue)]()
[![Architecture](https://img.shields.io/badge/architecture-adversarial%20multi--agent-orange)]()
[![Gatekeepers](https://img.shields.io/badge/human%20gatekeepers-0-red)]()

> Ask a single AI context to "consider three perspectives" and you get one voice wearing three hats — same blind spots, same biases, reviewing itself, and giving itself an A.
> **These skills don't ask nicely. They force isolation, force conflict, and force proof.**

⭐ **Star this if you've ever caught an AI confidently citing a source that doesn't exist — this is the fix.**

---

## Table of Contents

- [The Problem](#the-problem)
- [The Fix: Make Your AI Argue With Itself](#the-fix-make-your-ai-argue-with-itself)
- [How the Pipeline Actually Works](#how-the-pipeline-actually-works)
- [The Three Skills](#the-three-skills)
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

## The Problem

Every AI-generated document has the same original sin: **it's judge and defendant in the same trial.**

The model drafts the research. The model reviews the research. The model approves the research. Nobody in that loop has any incentive — or any *ability* — to disagree. So you get:

| What you were promised | What you actually get |
|---|---|
| "Three expert perspectives" | One voice, three fonts, same blind spots |
| "Peer-reviewed analysis" | Self-review — the writer marking its own exam |
| "Comprehensive coverage" | Overlapping sections quietly double-counting the same benefit |
| "Fully sourced" | Confident claims, zero primary sources, occasionally a fabricated citation |
| "Enterprise-ready spec" | A microservices architecture nobody asked for and nothing justifies |

None of this is a prompting problem. It's a **structural** problem. And you can't fix a structural problem by adding the word "please" to your prompt.

---

## The Fix: Make Your AI Argue With Itself

This repo contains **three production-grade agent skills** — `deep-research`, `brd-fsd-design`, and `tsd-design` — that all run on the same core belief:

> **Quality doesn't come from asking the model to "be careful." It comes from making it physically impossible to cut corners.**

Here's how each principle actually plays out:

### 🧱 Personas Are Exiled, Not Roleplayed
Every persona runs as its **own isolated sub-agent**, in its own tool session, with zero visibility into the others. Writing a persona's output inline instead of spawning a real, separate agent call is treated as a **critical failure** — the moment you fake isolation, three "perspectives" collapse back into one biased monologue.

### ⚔️ A Hostile Reviewer, Not a Yes-Man
Every draft faces a **CRITIC** sub-agent explicitly instructed to attack it — factual errors, unsupported claims, contradictions, missing angles, over-engineering. The CRITIC is deliberately kept blind to how the drafts were made. No search history. No internal reasoning. Just the finished work, judged cold. A soft "please review this" rubber-stamps everything — hostility isn't a personality quirk here, it's the entire QA mechanism.

### 🚫 Zero Human Babysitting
When something breaks, the pipeline doesn't shrug and ask you. It queries better data instead:
- CRITIC rejects it → re-dispatched to the exact persona with exact feedback
- Can't find a source → flagged as an honest "data gap," never invented
- A sub-agent times out → retried with reduced scope, not abandoned

It self-corrects for up to 3 rounds — then, if it still can't fix something, it **tells you that**, instead of hiding it.

### 🔲 Overlap Gets Hunted Down, Not Ignored
A structured 5-signal test — **Mechanism, Evidence, Problem, Benefit, Outcome** — runs across *every section pair, across every persona*, catching the double-counted benefits and contradictory recommendations before they ever reach you.

### 🎯 Confidence Is Earned, Never Assumed
Every output ships with an honest **HIGH / MEDIUM / LOW** confidence tag, based on how many fights the CRITIC actually won. Nothing ships pretending to be more certain than it is.

### 📎 Nothing Is Allowed to Be Orphaned
Every claim traces to a citation. Every business requirement traces to a functional requirement, to an acceptance criterion, to a test case. A broken link in that chain isn't a nitpick — it's a rejected draft.

---

## How the Pipeline Actually Works

All three skills run the **identical 5-phase architecture** underneath — only the cast of characters and the paperwork change.

```
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
```

**The one rule that can't be broken:** every persona and every review is its own tool call. The instant you simulate a persona inline instead of actually spawning it, the whole quality guarantee evaporates.

---

## The Three Skills

One of these skills is a generalist. Two are specialists. Know which one you're reaching for:

| Skill | What It Produces | Who's in the Room | Reach for This When |
|---|---|---|---|
| 🔬 [`deep-research`](./deep_research.md) | Multi-perspective research report on **any topic** | 3 experts, **auto-cast by the AI itself** based on what the topic needs | You need real research on something new — a market, a technology, a regulation — and don't know in advance who the "right" three experts even are |
| 📋 [`brd-fsd-design`](./brd-fsd-design.md) | BRD/FSD (23-section fixed structure) | Stakeholder · Compliance · Operator — **always these three** | You're tired of requirements docs full of "the system should be user-friendly" |
| 🏗️ [`tsd-design`](./tsd-design.md) | Technical Spec Document (24-section fixed structure) | Stakeholder · Compliance · Technical Architect — **always these three** | You have a BRD/FSD and need architecture that doesn't reinvent Kubernetes for a to-do app |

> Chain `brd-fsd-design` → `tsd-design` and go from raw business need to implementation-ready architecture, with an adversarial gate at every handoff. `deep-research` stands alone — point it at any subject.

### 🔬 Deep Research — General-Purpose, Self-Casting
This is the odd one out, deliberately. There's no fixed "Stakeholder/Compliance/Operator" cast here, because a general research topic doesn't have universal roles the way a business requirements doc does. Instead, the pipeline's own **STORM planning phase reads the topic first and invents the right three experts for it** — a crypto research question gets a different cast than a supply-chain question, which gets a different cast again than a regulatory question. Each self-identified persona then goes off in total isolation to do real, independent research — and a hostile CRITIC still tears the combined draft apart looking for factual errors, redundant sections, and claims that don't survive a source check. Includes hardened rules for jurisdictional/regulatory claims: no persona gets to *assume* a rule — they have to find it.

### 📋 BRD/FSD Design — Fixed Roles, Fixed Structure
Unlike `deep-research`, the cast here is locked: Stakeholder, Compliance, Operator, every time. Business requirements docs don't need a novel cast per project — they need the same three lenses applied with merciless discipline. A locked 23-section structure and unforgiving requirement hygiene: every requirement gets a unique ID, has to describe exactly one behavior, and gets rejected outright if it says "fast" or "user-friendly" without a number attached. Every business requirement has to prove it leads somewhere — to a functional requirement, to a testable acceptance criterion.

### 🏗️ TSD Design — Fixed Roles, Fixed Structure
Same logic as `brd-fsd-design`: Stakeholder, Compliance, Technical Architect, always. Takes an approved BRD/FSD and turns it into a real architecture — with two extra weapons the CRITIC uses:
- **The Build-vs-Reuse Ladder** — the Technical Architect has to justify, every single time, why they're building something new instead of reusing what already exists.
- **The Over-Engineering Audit** — the CRITIC actively hunts for unjustified microservices and abstraction layers nobody's requirement asked for. The one thing it will never let you cut for simplicity: security controls.

---

## Skill Comparison

| Dimension | `deep-research` | `brd-fsd-design` | `tsd-design` |
|---|:---:|:---:|:---:|
| Version | 1.0.0 | 1.1.0 | 1.0.0 |
| Domain | **General-purpose — any topic** | Business requirements | Technical architecture |
| Cast of personas | 🎭 **Self-identified per topic** by STORM planning | 🔒 Fixed: Stakeholder/Compliance/Operator | 🔒 Fixed: Stakeholder/Compliance/Tech Architect |
| Structure | 🎨 Custom outline, designed per topic | 🔒 Fixed 23 sections | 🔒 Fixed 24 sections |
| Hostile CRITIC | ✅ | ✅ | ✅ + over-engineering audit |
| MECE overlap check | ✅ | ✅ | ✅ |
| Traceability | Citations | BR → FR → AC | BR → FR → NFR → Component → Test |
| Confidence tag | ✅ | ✅ | ✅ |
| Max rematches | 3 | 3 | 3 |
| Needs input first | Just a topic | Business context | An approved BRD/FSD and/or NFRs |

> **Why the difference?** `deep-research` operates in an open domain — the "right" experts for "impact of tariffs on semiconductor supply chains" are not the same as for "clinical trial design for a new therapy." So it can't lock a cast; it has to *reason about who should be in the room* before it can even start. `brd-fsd-design` and `tsd-design` operate in a closed, well-defined domain — every business requirements doc and every technical spec benefits from the same three lenses — so locking the cast and the structure removes variance instead of adding it.

---

## This vs. a Normal Prompt

| | "Act as three experts" prompt | This Pipeline |
|---|---|---|
| Perspectives | Same context, same biases, different fonts | Physically separate agents, separate tools, zero shared memory |
| Review | The writer marks its own homework | A blind, hostile third party that wants to find something wrong |
| Overlap | Nobody notices until a human does | A 5-signal test run on every section pair, automatically |
| Missing sources | Shipped anyway, confidently | Flagged as a "data gap" — never faked |
| Structure | Whatever mood the model's in | Locked, enforced, no drift (or intentionally custom for `deep-research`) |
| Confidence | Implied by tone | Explicit, earned, and honest when it's low |
| Dead ends | Stops and asks you | Retries with better data, on its own |

---

## Installation

Each skill is a self-contained Markdown definition (YAML frontmatter + instructions), built for any agent runtime with sub-agent delegation and `web` / `terminal` / `file` toolsets.

```bash
git clone https://github.com/<your-username>/<your-repo>.git

# Drop the ones you want into your agent's skills directory
cp deep_research.md      ~/.your-agent/skills/deep-research/SKILL.md
cp brd-fsd-design.md     ~/.your-agent/skills/brd-fsd-design/SKILL.md
cp tsd-design.md         ~/.your-agent/skills/tsd-design/SKILL.md
```

> Built for Claude Agent Skills–style manifests and any orchestrator that exposes a `delegate_task(goal, context, toolsets)` primitive.

---

## Usage

No special syntax. Just describe what you need — each skill activates on natural-language triggers.

**Deep Research** (any topic — the AI casts its own experts)
```
"Do a deep-research report comparing stablecoin settlement options for cross-border payroll."
```

**BRD/FSD Design** (fixed Stakeholder/Compliance/Operator cast)
```
"I need a BRD/FSD for an automated invoice reconciliation system."
```

**TSD Design** (fixed Stakeholder/Compliance/Tech Architect cast — feed it the output of brd-fsd-design)
```
"Here's the approved BRD/FSD [attached]. Generate the TSD / technical architecture document."
```

Every run produces **one** finished Markdown document — executive summary, CRITIC's sign-off, honest confidence tag, unified references. No fragments, no loose ends, one single source of truth.

---

## Repository Structure

```
.
├── skills/deep_research.md       # Skill: General-purpose, self-casting research pipeline
├── skills/brd-fsd-design.md      # Skill: Business Requirements & Functional Spec pipeline
├── skills/tsd-design.md          # Skill: Technical Specification pipeline (consumes BRD/FSD)
└── README.md
```

---

## What You Actually Get

Every deliverable these skills produce comes with receipts:

- ✅ A **CRITIC Sign-Off** — a paper trail of exactly what got attacked and what got fixed
- ✅ An honest **confidence tag** — you know precisely how much scrutiny it survived
- ✅ **Inline citations** on every non-obvious claim, primary sources preferred
- ✅ **"Data gap" flags** instead of fabricated facts, wherever evidence didn't exist
- ✅ Full **traceability** from requirement → build → test (`brd-fsd-design` / `tsd-design`)

---

## FAQ

**"Can't I just tell the model to review its own work carefully?"**
You can ask. It won't disagree with itself. Self-review has zero adversarial pressure — it's the same context grading its own exam and giving itself full marks. That's the exact failure this repo exists to kill.

**"Why not just prompt 'act as three experts'?"**
Because roleplaying shares one context, one memory, one set of biases. Three "perspectives" from the same context quietly converge into one voice within a few paragraphs. Real isolation — separate sub-agents, separate tool sessions — is the only way to guarantee they actually disagree when they should.

**"Why does `deep-research` invent its own personas while the other two don't?"**
Because business requirements and technical architecture are closed domains — every project benefits from the same Stakeholder/Compliance/Operator (or Technical Architect) lenses, so locking them removes guesswork. General research is an open domain — the right experts for a legal question aren't the right experts for a market-sizing question. So `deep-research`'s planning phase looks at your specific topic first and designs the cast before any research begins.

**"What if the CRITIC never approves?"**
It gets 3 rounds to make its case. After that, the pipeline ships anyway — clearly labeled **LOW confidence**, with every unresolved objection listed in plain sight. It never pretends, and it never freezes waiting on you.

**"Can I run `tsd-design` on its own?"**
It expects an approved BRD/FSD and/or NFR document going in. Run `brd-fsd-design` first if you don't have one yet.

---

## Contributing

Issues and PRs welcome — especially:
- New domain-specific tuning for `deep-research`'s persona-casting logic
- New fixed-structure variants (PRD, RFC, etc.) built on this same pipeline
- Sharper MECE / over-engineering detection heuristics
- Real-world failure reports (timeouts, weird routing-loop edge cases)

Open an issue describing the failure before submitting big structural PRs — the rigidity (fixed structures, fixed personas in `brd-fsd-design`/`tsd-design`) is intentional, so changes should extend the pipeline, not loosen it.

---

## License

**MIT License** — Fork it, ship it, put it to work in your own agent stack.

---

<div align="center">

### Your AI shouldn't be the only one checking its own work.

**⭐ Star this repo** — it's the fastest way to help the next person find a pipeline that actually fights for the truth instead of assuming it.

</div>