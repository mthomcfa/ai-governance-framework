# FINOS Contribution Ideas: Subject-Matter PRs Across the Ecosystem

This document proposes worthwhile pull requests across FINOS repositories that leverage
AI governance, risk management, regulatory compliance, and financial services domain
expertise -- contributions that are more subject-matter than deep-code.

---

## 1. `finos/common-cloud-controls` -- Add AI-Specific Cloud Controls for Financial Services

**Repo:** [common-cloud-controls](https://github.com/finos/common-cloud-controls) (79 stars, 67 forks, active)

**What:** The CCC project defines cybersecurity, resiliency, and compliance controls for
cloud deployments in financial services. It currently covers common cloud services (object
storage, vector databases, etc.) but lacks explicit controls for **AI/ML workloads** running
on cloud infrastructure -- a rapidly growing use case in FS.

**Proposed PR:** The CCC already has `catalogs/ai-ml/gen-ai/` and `catalogs/ai-ml/mlde/`
directories. The MLDE (ML Development Environment) catalog has **an empty `threats.yaml`**
-- zero threats defined. Concrete contributions:
- Fill in `catalogs/ai-ml/mlde/threats.yaml` with MLDE-specific threats (model theft,
  training data exfiltration, compute hijacking, model poisoning during development)
  mapped to MITRE ATLAS and OWASP ML Top 10
- Add FINOS-AIGF mappings to `catalogs/ai-ml/mlde/controls.yaml` (the GenAI catalog
  has these but MLDE was missed -- see closed issues #872-876 for the pattern)
- Fill in five `'TODO: Describe this control family'` placeholders in MLDE controls
- Propose new GenAI controls for gaps: model inventory/registry, bias and fairness
  testing, human-in-the-loop, data retention/right-to-deletion, third-party model
  due diligence

**Why this fits:** Your AI Governance Framework already defines 23+ mitigations and risk
items that map directly to cloud control language. The CCC uses structured YAML formats
similar to what you already produce. Related open issues: #924, #925, #926 (control
definition questions for vector stores). Closed issues #872-876 (CC4AI) show the exact
pattern for AIGF cross-mapping.

**Effort:** Medium -- the empty `threats.yaml` and TODO placeholders are low-friction
first contributions; new controls require working group discussion.

---

## 2. `finos/open-regtech-sig` -- AI Regulation Landscape Document

**Repo:** [open-regtech-sig](https://github.com/finos/open-regtech-sig) (44 stars, active SIG)

**What:** The Regulation Innovation SIG creates open-source solutions for regulatory and
compliance challenges. Issue #80 proposes an AML/Financial Crime Prevention Working Group,
and issue #17 tracks "Potential Projects, Use Cases and Tools." There is currently **no
dedicated document mapping the evolving AI regulatory landscape** (EU AI Act, NIST AI RMF,
UK AI Safety Institute guidance, MAS FEAT, etc.) for financial services.

**Proposed PR:** Contribute an "AI Regulatory Landscape for Financial Services" reference
document covering:
- Jurisdiction-by-jurisdiction summary of AI-specific regulations affecting FS
- Mapping of requirements to practical compliance activities
- Cross-references to the AI Governance Framework's risk items (ri-22 etc.)
- Timeline of upcoming regulatory deadlines

**Why this fits:** Your ri-22 (Regulatory Compliance and Oversight) already references
EU AI Act, FFIEC, NIST AI 600-1, and SR 11-7. This would be a natural extension of that
work into a broader reference for the RegTech community.

**Effort:** Medium-High -- substantial content authoring, but building on knowledge you
already have.

---

## 3. `finos/ai-readiness` -- Responsible AI Compass Contribution

**Repo:** [ai-readiness](https://github.com/finos/ai-readiness) (55 stars, 20 forks, active SIG)

**What:** Issue #115 proposes a "Responsible AI Compass (RAIC)" -- a set of key questions
organizations should consider when deploying AI responsibly. Issue #116 collects initial
references for responsible AI. Both are tagged with "RAI" and "Idea" labels but have not
been developed into concrete deliverables.

**Proposed PR:** Develop the Responsible AI Compass as a structured decision framework:
- Categorized question sets (data governance, fairness, transparency, accountability)
- Mapping to existing standards (ISO 42001, NIST AI RMF, EU AI Act obligations)
- Financial-services-specific considerations per question
- Scoring or maturity-level indicators

**Why this fits:** The AI Readiness SIG spawned your AI Governance Framework project.
Contributing back to the parent SIG with a practical FS-specific tool would strengthen
the connection between the two initiatives.

**Effort:** Medium -- the framework structure already exists in your head; this is
about formalizing it.

---

## 4. `finos/devops-automation` -- AI Model Governance in the SDLC Controls Framework

**Repo:** [devops-automation](https://github.com/finos/devops-automation) (76 stars, active working group)

**What:** Issue #261 proposes an "SDLC Common Controls Catalogue Framework," and the
working group (issue #285) is actively developing this. The framework focuses on
traditional software but does not yet address the **AI/ML model lifecycle** -- training,
validation, deployment, monitoring, and retirement of models as part of the SDLC.

**Proposed PR:** The actual control definitions live at **finos-labs/SDLC-Controls-Framework**
(early-stage, CC-BY-4.0 licensed). Issues #18 (Control Backlog) and #19 (Risk Domain
Backlog) are actively seeking new control definitions. Contribute:
- AI model development lifecycle controls (data preparation, training, evaluation)
- Model validation and approval gates (aligned with SR 11-7)
- Continuous monitoring and drift detection controls
- Model retirement and deprecation procedures
- Regulatory mapping (OCC, FFIEC, DORA, Basel) to SDLC controls

Also note: Issue #245 (Delivery Workflow Analysis) already discusses **AI agent governance
in DevOps** -- "which AI-suggested changes warrant approval, who should approve them, the
scrutiny level required compared to human developers." Your input would be directly valued.

**Why this fits:** Your framework's mitigations (mi-4 AI System Observability, mi-5
System Acceptance Testing, mi-10 AI Model Version Pinning, mi-11 Human Feedback Loop)
are directly applicable SDLC controls for AI systems.

**Effort:** Medium -- contribute a focused section to an active working group.

---

## 5. `finos/open-source-readiness` -- AI-Specific Open Source Governance Guide

**Repo:** [open-source-readiness](https://github.com/finos/open-source-readiness) (48 stars, active SIG)

**What:** The OSR SIG helps FS firms adopt open source. Open issues include #210
(Information Classification), #208 (Patents), and several "Body of Knowledge" articles
(#214-217). There is no guidance specific to **open-source AI models and datasets** --
which present unique governance challenges (model licenses like RAIL, dataset provenance,
fine-tuning IP implications, EU AI Act transparency requirements for foundation models).

**Proposed PR:** Multiple high-value contributions possible here. The OSR BoK has a
`docs/bok/Regulations/` section covering AML, Cyber-Security (DORA/CRA), IP, etc.
but **no article on AI regulation**. Also, the `docs/bok/Risks/` section has 8 risk
types but **no AI-specific risk article**. Concrete options:
- New article `docs/bok/Regulations/AI-Regulation.md` covering EU AI Act, NIST AI RMF,
  SR 11-7, FCA/PRA expectations, MAS FEAT, and how these intersect with open-source AI
- New article `docs/bok/Risks/AI-Model-Risk.md` covering model provenance, training
  data bias, supply chain attacks on model weights, and reproducibility challenges
- Expand the Strategy article (currently just "THIS IS A PLACEHOLDER") with AI/ML
  open-source adoption strategy content (issue #205)
- Author a BoK article on open-source AI governance for FS (issues #210, #208)

**Why this fits:** FINOS identified "mutualizing AI adoption" as a 2025 strategic priority.
The OSR BoK has obvious gaps where AI governance content should exist, and your AIGF work
is directly relevant. The SIG meets first Wednesday of each month -- welcoming community.

**Effort:** Medium -- article-format contributions following existing BoK templates.
Multiple small PRs possible rather than one large one.

---

## 6. `finos/common-domain-model` -- AI Use Case Representations in CDM

**Repo:** [common-domain-model](https://github.com/finos/common-domain-model) (235 stars, 115 forks, very active)

**What:** The CDM standardizes how financial products, trades, and lifecycle events are
represented. It has active working groups for Collateral, Derivatives, Tokenized Assets,
and Physical Risk -- but no coverage of **AI-driven decision artifacts** in the trade
lifecycle (e.g., AI-generated credit assessments, algorithmic trade recommendations,
AI-based risk scores).

**Proposed PR:** Propose documentation or a discussion paper on how AI decision outputs
could be represented within CDM:
- Data model considerations for AI-generated risk assessments
- Audit trail and explainability metadata for AI decisions in trade workflows
- Mapping to regulatory reporting requirements (MiFID II, SR 11-7)
- Traceability of AI model version to specific trade decisions

**Why this fits:** Your use cases (credit risk analysis, autonomous wealth management)
generate exactly the kind of decision artifacts that would need CDM representation.
Issue #102 (ISO 20022 Mappings) shows the CDM community values standards interoperability.

**Effort:** Medium-High -- requires understanding CDM modeling conventions, but the
subject-matter contribution is focused on requirements, not code.

---

## 7. `finos/zenith` -- AI Governance Primer for Emerging Technologies

**Repo:** [zenith](https://github.com/finos/zenith) (27 stars, active SIG)

**What:** The Zenith Emerging Technologies SIG develops "primers" -- educational materials
on new technologies for the fintech ecosystem. They have a `primers/` directory and a DLT
primer, but **no AI governance primer** exists despite AI being the most impactful
emerging technology in financial services.

**Proposed PR:** Author an AI Governance Primer for the Zenith collection:
- Overview of the AI landscape relevant to FS (foundation models, agents, RAG, etc.)
- Key governance challenges unique to financial services
- Risk taxonomy summary (drawing from your 23 identified risks)
- Regulatory landscape overview
- Decision framework for evaluating AI adoption readiness
- References to the FINOS AI Governance Framework and AI Readiness SIG

**Why this fits:** Zenith explicitly seeks subject-matter expert "Brain Trust" members
and educational content. Issue #139 asks for community input on their website redesign,
and new primer content would be highly valued. This also promotes the AIGF more broadly
within FINOS.

**Effort:** Medium -- primer format is well-defined; you'd be adapting existing knowledge
for a broader audience.

---

## 8. `finos/InnerSource` -- InnerSource Patterns for AI/ML Teams in Financial Services

**Repo:** [InnerSource](https://github.com/finos/InnerSource) (33 stars, active SIG with new energy)

**What:** The InnerSource SIG promotes internal open-source practices within FS
organizations. Issue #158 asks to "Define Goal of SIG," and issue #167 requests adding
value metrics and resources. **AI/ML teams** are a natural but undocumented use case for
InnerSource practices -- they often need to share models, training data, and governance
artifacts across organizational boundaries.

**Proposed PR:** Contribute an InnerSource pattern or case study document:
- Why AI/ML teams benefit from InnerSource (shared model registries, common evaluation
  frameworks, reusable governance artifacts)
- InnerSource patterns for AI model governance (internal model marketplaces, peer review
  processes for model validation)
- Addressing compliance barriers to internal model sharing
- Metrics for measuring InnerSource success in AI/ML contexts

**Why this fits:** Chamindra de Silva (Citi) is active in both InnerSource and your
AI Governance Framework -- there is a direct community connection. The SIG is actively
seeking direction (issue #158) and this would be a concrete contribution.

**Effort:** Low-Medium -- pattern/case study format, drawing on your experience with how
FS firms manage AI internally.

---

## 9. `finos/architecture-as-code` -- CALM Architecture Pattern for AI-Governed Systems

**Repo:** [architecture-as-code](https://github.com/finos/architecture-as-code) (309 stars, 104 forks, very active)

**What:** The Architecture as Code project uses CALM (Common Architecture Language Model)
to describe system architectures in machine-readable format. It includes patterns and
examples but has no **reference architecture pattern for AI-governed systems** in financial
services -- despite having a "CALM AI" component.

**Proposed PR:** CALM has a `calm/controls/` directory with five domains (Security,
Performance, **Compliance**, Operational, Quality) -- but **all are empty** (just a
README framework with zero actual control definitions). Concrete contributions:
- **Populate the Compliance controls domain** with financial services regulatory controls
  (data residency, audit trail retention, regulatory reporting, model risk management,
  third-party risk). This would be the first real content in the controls framework.
- Contribute to issues #1410 and #1411 (evidence-to-control mapping design) -- your
  regulatory evidence expertise (SOC 2, PCI-DSS, SR 11-7, internal audit) is exactly
  what the schema designers need
- Author a CALM architecture pattern for a governed AI system in FS (RAG-based credit
  analysis with governance control points, threat model overlay, compliance metadata)
- Contribute to governance proposals #2318/#2319 (labeled `needs-input`) on project
  restructuring and decision-making processes

**Why this fits:** You already have detailed use case architectures (credit risk analysis,
wealth management) with threat models and control points. The empty controls framework is
a greenfield opportunity -- your contribution would literally be the first of its kind.

**Effort:** Medium -- the empty controls framework is low-friction; the architecture
pattern requires learning CALM JSON Schema.

---

## 10. `finos/financial-objects` -- AI Model Metadata as a Financial Object

**Repo:** [financial-objects](https://github.com/finos/financial-objects) (44 stars)

**What:** The Financial Objects SIG defines standard data objects for the FS industry. Open
issues include #104 (Financial Data Exchange), #103 (XBRL), and #102 (ISO 20022 Mappings).
AI models are increasingly becoming **critical financial infrastructure** but there is no
standard object definition for AI model metadata in the financial services context.

**Proposed PR:** Propose an AI Model Card / AI System Card as a financial object:
- Standard fields for AI system identification (model type, version, provider)
- Risk classification fields (EU AI Act risk category, internal risk tier)
- Performance and validation metrics
- Data governance metadata (training data sources, sensitivity classification)
- Regulatory compliance attestation fields
- Operational metadata (deployment environment, monitoring endpoints)

**Why this fits:** Your data classification framework (from the use cases) and risk
taxonomy provide the exact domain knowledge needed. Issue #104 (Financial Data Exchange)
suggests the SIG is open to new object definitions.

**Effort:** Medium -- conceptual/documentation work following existing object templates.

---

## 11. `finos/morphir` -- Business Rules for AI Governance as Morphir Models

**Repo:** [morphir](https://github.com/finos/morphir) (190 stars, 65 forks, active)

**What:** Morphir captures business logic as data, making it portable and executable across
platforms. It explicitly targets "regulatory technology applications for compliance and
governance." However, there are no **AI governance decision rules** modeled in Morphir --
despite governance decisions (risk classification, use-case approval, control selection)
being ideal candidates for formalization.

**Proposed PR:** Contribute a Morphir use-case example or documentation showing how AI
governance decisions could be modeled:
- Risk classification decision logic (mapping system characteristics to risk levels)
- Control selection rules (given a risk profile, which mitigations apply?)
- Regulatory applicability rules (given jurisdiction + use case, which regulations apply?)
- Use-case approval workflow logic

**Why this fits:** Your heuristic assessment framework and risk-to-mitigation mappings
are essentially business rules that could be formalized. Morphir's community actively
seeks financial services domain examples (per their README).

**Effort:** Medium -- conceptual modeling contribution; Morphir team would likely help
with the technical implementation.

---

## 12. `finos/OSLC-handbook` -- AI Model Licensing Guidance

**Repo:** [OSLC-handbook](https://github.com/finos/OSLC-handbook) (137 stars, 43 forks)

**What:** The Open Source License Compliance Handbook provides practical guidance for
complying with common open-source licenses. It is well-established but does not address
the **emerging landscape of AI model licenses** -- which use novel constructs not found
in traditional software licenses (use restrictions, responsible AI clauses, output
ownership terms).

**Proposed PR:** Contribute a new chapter or appendix on AI model licensing:
- Overview of common AI model licenses (RAIL, Llama license, Gemma terms, etc.)
- How AI model licenses differ from traditional software licenses
- Compliance considerations specific to FS (can you use model X for credit decisions?)
- Use-restriction analysis for common FS use cases
- Guidance on fine-tuning and derivative model licensing

**Why this fits:** Your ri-23 (Intellectual Property and Copyright) directly covers
these concerns. The handbook format is pure documentation/guidance -- no code required.

**Effort:** Medium -- requires careful analysis of AI model licenses, but aligns with
your existing IP risk work.

---

## 13. `finos/community` -- Cross-Project AI Governance Resource Map

**Repo:** [community](https://github.com/finos/community) (75 stars, 36 forks)

**What:** The FINOS community repo is the central collaboration space across all projects
and SIGs. Currently, AI-related work is spread across multiple repos (ai-readiness,
ai-governance-framework, aigf-mcp-server, open-regtech-sig, zenith) with **no unified
map** showing how these initiatives connect and where contributors should go for what.

**Proposed PR:** Create an "AI at FINOS" resource guide:
- Map of all AI-related FINOS projects and SIGs with their focus areas
- Decision tree: "I want to contribute to AI governance in FS -- where do I start?"
- Cross-reference matrix showing how projects relate to each other
- Summary of open contribution opportunities across the AI ecosystem
- Links to mailing lists, meeting calendars, and key contacts

**Why this fits:** As someone active in the AI Governance Framework and familiar with the
broader FINOS ecosystem, you're uniquely positioned to create this map. It would also
raise the profile of the AIGF and encourage cross-pollination.

**Effort:** Low-Medium -- curation and documentation work.

---

## 14. `finos/FDC3` -- AI/LLM Governance for the Financial Desktop Standard

**Repo:** [FDC3](https://github.com/finos/FDC3) (249 stars, 168 forks, very active)

**What:** FDC3 is the open standard for desktop application interoperability on financial
trading desks. Issue #1713 ("Enhance FDC3 standards for LLMs") proposes enriching the
AppDirectory and intent metadata so LLMs can select published intents as tools -- directly
relevant to agentic AI governance. Issue #1816 (Use Cases and Workflows group) is actively
mapping AI/LLM integration patterns including "auditable human involvement" requirements.

**Proposed PR:** Contribute AI governance use cases and a compliance context type:
- Use-case document for #1713 mapping specific FS workflows (trade surveillance,
  compliance checking, client suitability) where LLMs interact with FDC3 intents, with
  governance guardrails (human-in-the-loop, audit trails, explainability)
- Propose a new FDC3 context type (e.g., `fdc3.compliance.auditTrail`) capturing the
  provenance of AI-suggested actions for regulatory compliance
- Risk and governance framework for AI-FDC3 integration covering data sovereignty,
  SR 11-7 alignment, and supervisory expectations for automated intent resolution

**Why this fits:** Your agentic AI risks (ri-24 through ri-29) covering agent authorization,
tool-chain manipulation, and multi-agent trust boundaries directly apply to LLMs invoking
FDC3 intents on trading desks. This is a high-visibility, standards-setting contribution.

**Effort:** Medium -- requires understanding FDC3 context/intent model, but the governance
content is your core expertise.

---

## Summary Table

| # | Repo | PR Idea | Type | Effort |
|---|------|---------|------|--------|
| 1 | common-cloud-controls | Fill empty MLDE threats + AI cloud controls | Control definitions | Medium |
| 2 | open-regtech-sig | AI regulatory landscape document | Reference doc | Medium-High |
| 3 | ai-readiness | Responsible AI Compass framework | Decision framework | Medium |
| 4 | devops-automation | AI model governance in SDLC controls | Framework extension | Medium |
| 5 | open-source-readiness | AI regulation + risk BoK articles | BoK articles | Medium |
| 6 | common-domain-model | AI decision artifacts in CDM | Discussion paper | Medium-High |
| 7 | zenith | AI governance primer | Educational primer | Medium |
| 8 | InnerSource | InnerSource patterns for AI/ML teams | Pattern doc | Low-Medium |
| 9 | architecture-as-code | Populate empty CALM compliance controls | Control definitions | Medium |
| 10 | financial-objects | AI Model Card as financial object | Object definition | Medium |
| 11 | morphir | AI governance rules as Morphir models | Use-case example | Medium |
| 12 | OSLC-handbook | AI model licensing guidance | Handbook chapter | Medium |
| 13 | community | Cross-project AI resource map | Community guide | Low-Medium |
| 14 | FDC3 | AI/LLM governance for trading desk standard | Standards/use cases | Medium |

---

## Recommended Prioritization

**Quick wins (lowest friction, highest immediate impact):**
1. **#1 - common-cloud-controls: Fill empty MLDE threats.yaml** -- Literally empty file
   waiting for content; follows established GenAI catalog pattern
2. **#13 - community: AI Resource Map** -- Low effort, high visibility curation work
3. **#9 - architecture-as-code: Populate empty CALM compliance controls** -- Greenfield
   controls framework with zero content; your contribution would be first-of-kind

**High-value, moderate effort:**
4. **#3 - ai-readiness: Responsible AI Compass** -- Direct parent SIG, open issue waiting
5. **#5 - open-source-readiness: AI Regulation BoK article** -- Obvious gap, template exists
6. **#4 - devops-automation: AI in SDLC** -- Active working group, issues explicitly
   waiting for AI governance input
7. **#14 - FDC3: AI/LLM governance for trading desks** -- High-visibility standards work,
   issues #1713 and #1816 explicitly need AI governance perspective

**Strategic, longer-term:**
8. **#7 - zenith: AI Governance Primer** -- Reuses existing knowledge broadly
9. **#2 - open-regtech-sig: AI Regulatory Landscape** -- Substantial but high value
10. **#12 - OSLC-handbook: AI Model Licensing** -- Unique expertise needed
11. **#10 - financial-objects: AI Model Card** -- Novel standard contribution
12. **#8 - InnerSource: AI/ML Patterns** -- Community connection exists

---

*Generated April 2026 by researching 180+ FINOS repositories and cross-referencing with
the AI Governance Framework's risk taxonomy, mitigation catalog, and use-case library.*
