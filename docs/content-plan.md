# Personal Homepage — Content Plan

Target: <https://thex1ay.github.io> · Repo: `TheX1ay/TheX1ay.github.io`

Working document. Delete or move to a private repo before launch if preferred.

---

## 1. Positioning

The site has to answer three questions in under ten seconds:

1. **Who is this?** — Haohan Xue
2. **What do they work on?** — question answering over virtual knowledge graphs;
   LLM agents that fail silently and how to make them abstain instead.
3. **What do I do next?** — read a paper, open a repo, send an email.

Everything else on the page is supporting evidence for those three.

**Audience priority** (drives tone and ordering):

| Rank | Audience | What they came for |
|---|---|---|
| 1 | Prospective advisors / hiring committees | Publications, research taste, CV |
| 2 | Researchers in KG / Text-to-SPARQL / LLM agents | Papers, code, datasets |
| 3 | Recruiters, general visitors | One-paragraph identity |

Language: **English**, single language. Chinese-only pages read as local; this
page's audience is international. (Can add a `/zh` mirror later if wanted.)

---

## 2. Information architecture

Single scrolling page, no nav needed beyond anchor links. Six sections, ordered
by what a reader actually needs, not by what is easiest to write.

```
┌─ Hero ──────────────── name · positioning line · affiliation · 5 links
├─ About ─────────────── 3–4 sentences, first person, no buzzwords
├─ Research ──────────── research statement + 2 project cards w/ figures
├─ Publications ──────── 2 entries, each with [Paper] [Code] [BibTeX]
├─ Projects ──────────── 4–5 repos, auto-pulled metadata
├─ News ──────────────── 3–5 dated one-liners (optional at launch)
└─ Footer ────────────── email, last-updated, ©
```

Deliberately **excluded** for now: blog (no posts yet — an empty blog is worse
than none), teaching, awards, photo (add only if a good one exists; a bad photo
costs more than no photo).

---

## 3. Section-by-section draft copy

### Hero

> **Haohan Xue**
> I study how LLM agents fail *quietly* on knowledge graphs — and how to make
> them say "I don't know" instead of returning a confident wrong answer.
>
> `[Email]` `[GitHub]` `[Google Scholar]` `[CV]` `[ORCID]`

Rationale: the second line is the whole site. "Silent failure" is concrete,
slightly counterintuitive, and immediately distinguishes this page from the
thousand "I am passionate about AI" homepages. It also happens to be literally
what the two papers are about, so the hook is not marketing — it is the thesis.

Affiliation line goes directly under the name once confirmed (see §5).

### About

> I am a researcher working on question answering over **virtual knowledge
> graphs** (VKGs), where a SPARQL query can be syntactically valid, execute
> without error, and still return a wrong or empty answer. My work treats these
> *silent failures* as the central problem rather than an edge case: I build
> pipelines that diagnose why a query failed, verify candidates before trusting
> them, and abstain when no reliable signal exists.
>
> More broadly I am interested in evaluation and reliability of LLM agents on
> structured data — the gap between "the system ran" and "the system was right".

Draft, to be edited to match reality. Keep it under 120 words; the longer story
belongs in the research section.

### Research

Three short subsections, each 2–4 sentences, each ending in a link:

**1. Navigating virtual knowledge graphs**
The active-ontology pipeline: build an ontology view, link question elements,
expand candidate subgraphs iteratively, rerank, then emit SPARQL. Motivation:
the mapping layer does not cover every predicate, so retrieval — not generation
— is where these systems break.
→ `Navigate-VKG`

**2. Triaging silent failures**
ATTEST routes each failure by the diagnostic signal it exposes: sparse ontology
targets go to iterative repair, dense targets to a single-shot direct probe;
a deterministic zero-LLM verifier catches AST-level errors; failures with no
usable signal are *admitted* rather than retried. Successful repairs are indexed
by query skeleton and error-code multiset for cross-structure transfer.
→ `ATTEST`

**3. Reliability of retrieval over structured data**
CGRAG4VKG — graph-based retrieval augmentation for VKG question answering.

Each subsection can carry one figure (framework diagrams already exist in the
repos at `figures/framework.png`).

### Publications

Format per entry — venue/year **must be filled in, not guessed**:

```
ATTEST: Abstention and Trustworthy Evidence for Silent-failure Triage
in Virtual Knowledge Graph Question Answering
Haohan Xue.
[venue, year]
[Paper] [Code] [BibTeX]
```

Ordering: reverse chronological. If either is under review, mark it honestly
(`Under review, 2026`) — never present a preprint as accepted.

BibTeX should be a collapsible `<details>` block, copyable in one click. This
is the single most-appreciated feature on an academic homepage and costs
nothing to build.

### Projects

Cards with: repo name, one-line description, language dot, stars, last commit.
Candidates from the account:

| Repo | Public? | Use on site |
|---|---|---|
| ATTEST | ? | Yes — flagship |
| Navigate-VKG | ? | Yes — flagship |
| CGRAG4VKG | ? | Yes |
| NaVQA | ? | Duplicate of Navigate-VKG — skip or merge |
| protein_predict | ? | Only if the protein thread is part of the story |
| PaperGod | ? | Only if it is presentable tooling |
| evolvepro-ce5 | ? | Probably skip (looks like a fork/experiment) |

Note: only 1 of 8 repos is currently public, so most links would 404 for
visitors. Decide per repo: make public, or omit from the site.

### News

Leave the section out at launch; add it the first time there is real news
(paper accepted, talk given, artifact released). An empty or stale news list
signals an abandoned page.

### Footer

Public email, "Last updated: <month year>", © year. A visible update date is a
credibility signal — it says the page is maintained.

---

## 4. Technical shape

**Recommendation: plain static HTML + one CSS file, no build step.**

- Deploy: Pages from `main` / root. Push = publish. No Actions, no npm, no
  lockfiles to rot.
- Why not a framework: the content is ~6 sections and changes a few times a
  year. A build pipeline buys nothing and adds a failure mode.
- Why not Jekyll/Astro yet: only worth it if a blog is added later; migrating
  one HTML file to Astro takes an hour when that day comes.
- Fonts: one serif for headings, one sans for body, self-hosted or system stack
  (avoid render-blocking Google Fonts on a page this small).
- Must-haves: `<meta>` OG tags for link previews, favicon, responsive down to
  360px, dark/light via `prefers-color-scheme`, print stylesheet (advisors do
  print these).

**Open decision:** dark-first or light-first. Research pages skew light; the
page should respect the OS preference regardless.

---

## 5. Information still needed

Cannot be invented — needs the owner:

1. **Affiliation / position** (university, lab, advisor, degree stage, dates)
2. **Public email** — `thex1ay2002@gmail.com` is in git config; is that the one
   to publish, or a institutional address?
3. **Google Scholar / ORCID / Semantic Scholar** profile URLs
4. **CV PDF** — exists? should it be downloadable?
5. **Publication venue + year** for ATTEST and Navigate-VKG
6. **Which repos to make public**
7. **Photo** — have one? willing to publish?
8. **Blog** — planned, or out of scope?

---

## 6. Design directions (to pick once the style skill is installed)

Four archetypes, all compatible with the content above:

- **A. Academic minimal** — serif headings, single column, max 68ch, near-zero
  chrome. Reads as a paper. Safest, most credible, ages well.
- **B. Editorial** — large display type, wide margins, one saturated accent.
  Feels designed; slightly higher risk of looking like a portfolio template.
- **C. Technical / terminal** — monospace accents, dark default, subtle grid.
  Fits systems-flavored work; can read as gimmicky if overdone.
- **D. Card-based product** — project cards with figures and hover states.
  Best if the repos are the main attraction.

Recommendation: **A as the base, borrowing D's project cards.** The content is
research-first, so the typography should carry it, but the two framework figures
deserve card treatment.

### Decision — 2026-11-03

Chose **`claude`** from `design-style-library` (67 styles surveyed, 4 finalists:
`claude`, `terracotta`, `refined`, `codex`).

Why: the brief is literally a *research-journal aesthetic* — warm ivory parchment
`#FAF9F6` instead of clinical white, near-black ink `#141413`, one earthy clay
accent held in reserve, zero shadows, hard edges, emphasis by typography and
underline rather than colour. That matches a page whose job is to be read, not
admired.

Rejected:

- `terracotta` — DM Serif Display reads as a lifestyle blog; undercuts seriousness.
- `refined` — Playfair Display is specified for *body* text; high-contrast serif
  at 16px is hard to read.
- `codex` — too empty to hold two framework figures.

Adaptations made while building (all noted in `assets/style.css`):

- `--ink-45` darkened `#7A776F → #6E6B64`: the original was 4.26:1 on paper and
  failed WCAG AA. Now 5.1:1.
- `--measure` reduced `66ch → 60ch`: 66ch measured 640px ≈ 75 characters, past
  the comfortable range.
- Dark mode does **not** flip the inverted band to ivory — a page-wide ivory
  block on near-black reads as a rendering fault. It becomes one elevated
  surface (`#1C1B19`) instead.

---

## 7. Build order

1. Confirm §5 answers
2. Pick design direction
3. Build `index.html` + `style.css` with real copy
4. Local preview, responsive + print check
5. Make repo public → enable Pages → verify live URL
6. Add OG image, favicon, sitemap
