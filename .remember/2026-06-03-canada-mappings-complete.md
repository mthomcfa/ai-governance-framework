# Memory — FINOS AIGF Canada Regulatory Mappings (Option C) — COMPLETE

**Date landed:** 2026-06-03
**Contributor:** mthomcfa (mthom@cfacanada.org)
**Status:** All deliverables shipped. Awaiting maintainer/steerco commentary.

---

## What this was

Contribute Canadian (CSA / CIRO / OSFI / OPC) regulatory mappings to the FINOS
AI Governance Framework. Strategy = **Option C**: ship the mapping work as **two
parallel PRs**, one on each competing data foundation, so maintainers and the
steering committee retain full optionality on which data PR to land — the mappings
arrive ready either way, and the unused one simply closes.

## The two data foundations (both upstream, not mine to merge)

- **#290** (mine): standalone `docs/_data/csa-ciro-canada.yml`, flat `{title,url,issuer}`.
- **#301** (pmerrison): consolidated `docs/_data/canada-regulations.yml`, sub-keyed
  `{title,url,issuer,description}`, 48 entries. Branch `pmerrison/canada-regulations-data`
  @ `e9a0a12`. Had 1 maintainer approval (alvin-c-shih, 2026-05-27). Consolidates the
  closed #285 (Luca Borella) + my #290.

## Deliverables shipped

| Item | State |
|---|---|
| Comment on #301 (sign-off + parallel-PR framing + B-10/IOSCO heads-up) | Posted 2026-06-02, renders clean |
| **Track A PR #318** — mappings on #290 foundation | OPEN (draft). `finos:main` <- `mthomcfa:canada-mappings-csa-ciro-risks` @ `590ca0d` |
| **Track B PR #319** — mappings on #301 foundation, stacked on #301 | OPEN. branch `canada-mappings-consolidated-risks` @ `891310d` (rebased onto pmerrison/canada-regulations-data and force-pushed) |

Both mapping commits authored `mthomcfa <166031097+mthomcfa@users.noreply.github.com>`,
DCO `Signed-off-by` present (FINOS requires DCO per CONTRIBUTING.md). GPG-unsigned
(sandbox couldn't sign); amend `-S` locally if a Verified badge is wanted.

## What each track changed

Both add `<dataset>_references:` front matter to **8 risk files** (ri-1, ri-2, ri-16,
ri-17, ri-18, ri-19, ri-20, ri-22) and wire the reference-card include into
risk.html + mitigation.html.

- **Track A**: `csa-ciro-canada.yml` 20 -> 32 entries. Per-risk ref counts:
  ri-22=21, ri-16=7, ri-17=11, ri-18=12, ri-19=11, ri-20=8, ri-1=13, ri-2=14.
- **Track B**: `canada-regulations.yml` 48 -> 60 entries (uses #301 sub-keys, so
  higher counts — finer vocabulary, same regulatory substance). Per-risk:
  ri-22=27, ri-16=7, ri-17=13, ri-18=12, ri-19=12, ri-20=8, ri-1=14, ri-2=15.

Net-new entries (both tracks, schema-translated): CIRO GN-2300-21-003, NI 81-102/106/107,
CSA SN 31-342, AMF AI Guideline, OSFI B-10, Quebec Law 25 ss. 12.1 & 3.3/17, CHRA,
Ontario HRC, IOSCO FR/02/2026 (replaces IOSCO CR/01/2025), + (Track B only) NI 31-103
s.14.2 sub-key.

## Regulatory accuracy points resolved (don't relitigate)

- **NI 81-102 s. 5.1(1)(c)** = "fundamental investment objectives changed" — CORRECT
  as cited. (Confirmed against NI 81-102 Part 5 text the user pasted. The adversarial
  reviewer's "should be (a)" was wrong — (a) is fee-basis; (d) is [repealed]. My own
  CP-only guess of "(d)" was also wrong. Source check settled it: (c) stands.)
- **OSFI B-10** = general, FRFI-only, NOT AI-specific third-party risk guideline
  (in force 2024-05-01). Corrected an earlier overclaim ("dominant Canadian benchmark
  for AI vendor governance"). Now framed: AI/model vendors fall within its third-party
  scope; E-23 (2027) leans on it for third-party model-vendor risk; persuasive only for
  CSA/CIRO registrants (their binding hooks are NI 31-103 s.11.1 + CIRO GN-2300-21-003).
- **IOSCO FR/02/2026** = real. Verified against IOSCOPD823 PDF: "Supervisory Toolkit
  for AI Use in Capital Markets," Final Report, IOSCO Board, May 2026, 5 focus areas
  (governance / third-party / disclosure / recordkeeping / monitoring). Supersedes
  CR/01/2025 (IOSCOPD788).
- **PIPEDA Schedule 1** = 10 principles (4.1-4.10). **Bill C-27/AIDA** died on the
  order paper, 44th Parliament (Jan 2025 prorogation); no successor as of 2026.

## Key decisions locked

- Keep Track B granular (use #301 sub-keys), not collapsed to parents.
- Tier 4 (privacy/human-rights statutes) included in the jurisdictional file as an
  explicit RFC to maintainers; admission criteria in the Tier 4 YAML header.
- Tier 4 issuer fields normalized to bare tokens (OPC/CAI/CHRC/OHRC), jurisdiction
  moved into titles/descriptions.
- Framing = "no rework whichever way you go" (soft reframe), NOT "optionality"
  (reviewers found the latter reviewer-hostile).
- Track B opened as a stacked PR on #301 (rebased onto pmerrison's branch) so his 48
  entries trace to HIS commits — correct attribution, not re-committed under my name.

## When commentary arrives — what to watch / be ready for

1. **Structural decision** (consolidate via #301 vs standalone #290): deferred to
   maintainers. Whichever data PR lands, rebase the matching mapping PR onto the new
   main (trivial, clean delta) and close the other mapping PR.
2. **Tier 4 RFC**: maintainers may want privacy/HR statutes split into a separate
   `canada-cross-cutting.yml`. Be willing to split; don't die on this hill.
3. **NI 31-103 s.13.3 reasonable-basis != explainability** (Claim 3): strongest framing
   claim, surface it if challenged on the ri-17 mapping or the ri-16 non-mapping.
4. **IOSCO swap on Track B**: flagged to pmerrison that CR was replaced by FR; restore
   CR if he prefers lineage.
5. **rationale-comment density** and **standalone-vs-consolidated**: have "happy to
   trim / happy to rebase whichever lands" responses ready.

## Environment notes (for resumption)

- This was a Claude Code on the web (cloud) session, scope-locked to
  `mthomcfa/ai-governance-framework` — could NOT read/write finos repo, post comments,
  or open PRs directly. All finos-side actions done by the user locally (gh / web UI).
- Local checkout that works for teleport: clone of the FORK (origin = mthomcfa).
  The OneDrive checkout had origin=finos/fork=mthomcfa (swapped), which blocked
  `claude --teleport`; user cloned fresh to %USERPROFILE%\code\ai-governance-framework.
- Source docs used (uploaded by user, not in repo): OSFI B-10 PDF, NI 81-102CP
  consolidation, NI 81-102 Part 5 text, IOSCOPD823 PDF, framing-notes-v2.md (= Track A
  PR body source), DRAFTmappings.md, data-file-additions.yml, reference-keys.md.

## Cross-links to post when convenient (low priority)

One comment each on #290, #301, #318, and #319 pointing at the others, so a
reviewer landing on any thread finds all four.
