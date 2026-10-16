# Business Justification: Self-Hosted Enterprise LLM Platform vs. Current In-House AI Tools

| Field | Value |
|---|---|
| Document status | DRAFT v0.1 – base material for a future formal report |
| Date | 2026-10-14 |
| Prepared for | [Sponsor / Decision Authority] |
| Prepared by | [Author] |
| Companion document | `01_Analysis_of_Alternatives_CUI_LLM_Platform.md` |

> **Note.** Figures marked *illustrative* are placeholders to demonstrate the calculation method. Replace them with measured values (user counts, hours, labor rates, license costs) before this document is used to request funding. Items in `[brackets]` need input.

---

## 1. Purpose

Justify investment in a dedicated, on-premises LLM platform authorized for CUI, compared with continued reliance on the two AI tools currently provided by [Organization] ("Tool A" and "Tool B").

## 2. Executive Summary

- The current tools are **functionally limited and constrained by small context windows**, so they cannot support the document-heavy, multi-step engineering workflows the organization needs (long specifications, multi-document comparisons, large codebases/scripts, report generation).
- Staff either **work around the limitations manually** (splitting documents, copy/paste, re-prompting), **abandon the tools**, or are tempted to **use unapproved external tools**, which is a CUI spill risk.
- A self-hosted platform provides **≥128K context**, an **API for automation**, **RAG over internal repositories**, **multi-user concurrency**, **customization**, and **full control of CUI data** within the existing authorization boundary.
- Estimated investment: **$125K–$300K capital** for the recommended initial tier plus ~$40–85K/year operating cost (see AoA, Tier B).
- *Illustrative* payback: **~12–20 months** if the platform returns 1.5–2.5 hours/week to each of 150 active users (Section 7).
- The strongest justification is not only cost: it is **enabling capabilities that are currently impossible** and **reducing data-handling risk**.

---

## 3. Current State

### 3.1 Existing Tools (complete the table)

| Attribute | Tool A: [name] | Tool B: [name] | Needed for target workflows |
|---|---|---|---|
| Hosting / owner | [ ] | [ ] | On-prem or accredited enclave |
| CUI authorized? | [ ] | [ ] | Yes (required) |
| Underlying model | [ ] | [ ] | Selectable, upgradable, auditable |
| Max context window | [e.g., 4K–32K] | [ ] | ≥128K (stretch 256K+) |
| Max output length | [ ] | [ ] | ≥4K–8K tokens |
| File/document upload limits | [ ] | [ ] | Large PDFs/spreadsheets/code repos |
| API / automation access | [ ] | [ ] | Yes (OpenAI-compatible) |
| RAG over internal data | [ ] | [ ] | Yes, with per-group access control |
| Concurrency / rate limits | [ ] | [ ] | Supports team-wide peak use |
| Fine-tuning / customization | [ ] | [ ] | LoRA / prompt libraries / custom tools |
| Code/script assistance quality | [ ] | [ ] | Strong |
| Audit logging | [ ] | [ ] | Per-user, exportable to SIEM |
| Cost model | [ ] | [ ] | Predictable |
| Roadmap control | None/vendor | None/vendor | Organization-controlled |
| Data retention / training on inputs | [ ] | [ ] | None; org-controlled retention |

### 3.2 Observed Pain Points (validate with user survey / interviews)
1. **Context limits** force splitting documents, losing cross-references and producing inconsistent answers.
2. **Limited functionality**: weak file handling, no custom tools, no scripting/API integration, no workflow chaining.
3. **Quality gaps** on technical reasoning, code, and long-form structured output.
4. **Low adoption/trust**: users stop using tools after poor results, so the existing investment yields little value.
5. **Shadow AI risk**: users may paste work content into unapproved public tools to get the capability they need.
6. **No ability to adapt** tools to organization terminology, templates or standards.

---

## 4. Proposed Solution (Summary)

An on-premises GPU-based inference platform running a portfolio of open-weight LLMs, with chat UI, OpenAI-compatible API, RAG over controlled repositories, SSO with MFA, and full audit logging, all inside the CUI boundary. See the AoA for architecture, tiers and sizing. Recommended starting point: **Tier B** (4× 96 GB GPUs; ~20–80 simultaneous active users; 128K context), scalable to Tier C.

---

## 5. Benefits

### 5.1 Capability Benefits (Why Existing Tools Cannot Substitute)

| Capability | Business value | Example workflow |
|---|---|---|
| **Large context (128K+ tokens ≈ 300+ pages)** | Analyze entire specs, contracts or test reports in one pass without chunking | Compare requirements in a 200-page spec against a test report and list gaps |
| **Multi-document RAG with citations** | Find and cite answers across thousands of internal documents | "What did past programs decide about connector X?" with source links |
| **API access** | Embed LLM into scripts, pipelines, CI, Excel/SharePoint workflows | Automated nightly summary of new anomaly reports |
| **Code and script assistance on large codebases** | Faster development, documentation, test generation, refactoring | Review a 20-file Python/MATLAB toolchain for defects and generate unit tests |
| **Multi-user concurrency with quotas** | Team-wide availability, fair sharing, predictable response | 50 engineers using the system simultaneously during peak |
| **Batch processing** | Bulk tasks run overnight | Classify/summarize 10,000 legacy records |
| **Customization / fine-tuning** | Learn terminology, templates, formats | Draft reports in the organization's standard format |
| **Model choice and upgrades** | Swap in better models as they appear; no vendor lock-in | Move to a new model release within days of approval |
| **Structured output / tool use** | Reliable JSON, forms, database queries | Auto-populate trace matrices |

### 5.2 Productivity Benefits
Typical knowledge-work tasks where LLM assistance produces measurable time savings (*published studies and vendor reports show wide ranges; validate in a pilot*):

| Task category | Baseline effort | Expected reduction | Note |
|---|---|---|---|
| Document summarization / review | 1–4 hr | 40–70% | Largest gain with long-context support |
| First-draft reports, emails, procedures | 1–3 hr | 30–50% | Human review still required |
| Information search across repositories | 0.5–2 hr | 50–80% | Needs RAG |
| Code/script writing, debugging, tests | varies | 20–40% | Strong for boilerplate/analysis tools |
| Data extraction/transformation | 1–6 hr | 40–80% | Via API/batch |
| Requirements/traceability analysis | 4–16 hr | 30–60% | Context window dependent |

### 5.3 Risk-Reduction Benefits
- **CUI containment:** processing stays inside the authorization boundary, with no third-party retention or training on inputs.
- **Reduced shadow-AI use:** providing a capable approved tool reduces the incentive to use unapproved ones.
- **Auditability:** per-user logs and retrieval records support compliance evidence and incident response.
- **Supply-chain control:** approved, hash-verified model inventory and a documented import process.
- **Continuity:** not dependent on a vendor changing pricing, terms, features or model availability.

### 5.4 Strategic Benefits
- Builds in-house AI engineering capability and a reusable internal platform.
- Provides a foundation for domain-specific assistants (test engineering, configuration management, proposals).
- Retains institutional knowledge by making historical documents searchable and usable.
- Supports future agentic workflows with controlled tools and permissions.

---

## 6. Costs (Summary)

Tier B reference estimates from the AoA (replace with quotes):

| Cost element | Estimate |
|---|---|
| Hardware (GPU server, app/RAG servers, storage, network, rack/UPS) | $125K–$210K (up to ~$300K with a second node/HA) |
| Integration, hardening, ATO documentation (one-time labor/contractor) | $30K–$100K |
| Software (open-source stack; OS/support subscriptions) | $5K–$25K/yr |
| Hardware support/warranty (10–15%/yr) | $15K–$30K/yr |
| Power and cooling (~4.5 kW continuous ≈ 39,000 kWh/yr) | $4K–$8K/yr at $0.10–0.20/kWh, before facility overhead |
| Operations/ML engineering (0.5–1.0 FTE equivalent) | $75K–$150K/yr loaded |
| **3-yr TCO (estimated)** | **$0.25M–$0.46M** |

**Costs of the status quo to include (fill in):** current license/subscription fees $[ ]/yr, support effort $[ ]/yr, productivity lost to limitations (Section 7), cost of any CUI incident or rework.

---

## 7. Financial Analysis (Method + Illustrative Example)

### 7.1 Formulas

$$\text{Annual benefit} = N_{\text{active}} \times H_{\text{saved/week}} \times W \times R \times E$$

where $N_{\text{active}}$ = active regular users, $H$ = hours saved per user per week, $W$ = working weeks per year (~46), $R$ = fully burdened labor rate ($/hr), and $E$ = realization factor (fraction of saved time converted to useful work; use 0.5–0.7 to be conservative).

$$\text{ROI} = \frac{\text{Total 3-yr benefit} - \text{Total 3-yr cost}}{\text{Total 3-yr cost}} \qquad \text{Payback (months)} = \frac{\text{Upfront cost}}{\text{Monthly net benefit}}$$

### 7.2 Illustrative Scenarios (*all inputs are placeholders*)

| Input | Conservative | Expected | Optimistic |
|---|---|---|---|
| Active users ($N$) | 100 | 150 | 250 |
| Hours saved / user / week ($H$) | 1.0 | 2.0 | 3.0 |
| Working weeks ($W$) | 46 | 46 | 46 |
| Burdened rate ($R$) | $100/hr | $100/hr | $100/hr |
| Realization ($E$) | 0.5 | 0.6 | 0.7 |
| **Annual benefit** | **$230K** | **$828K** | **$2.42M** |
| Annual run cost (OpEx incl. staff) | $130K | $130K | $160K |
| Upfront cost (CapEx + integration) | $300K | $300K | $450K (Tier C) |
| Existing tools cost avoided/retired (optional) | $[ ] | $[ ] | $[ ] |
| **Net annual benefit** | **$100K** | **$698K** | **$2.26M** |
| **Payback** | ~36 months | **~5 months** | ~2.4 months |
| **3-yr ROI** | ~0% | **~170%** | ~330% |

> The conservative case barely breaks even on time savings alone, which is why the capability and risk arguments (Section 5.1, 5.3) matter. Productivity savings are often not budget-recoverable "cash"; frame them as **capacity gained** (more throughput without added headcount) unless a headcount or contract-cost impact can be shown.

### 7.3 Sensitivity Highlights
- **Biggest driver:** hours saved per user per week. Each additional 0.5 hr/week across 150 users at $100/hr and $E$ = 0.6 is worth ≈ **$207K/yr**.
- **Adoption:** benefits scale with *active* users; plan training and champions to reach target adoption.
- **Utilization:** under-utilized GPUs raise cost per user; over-utilization degrades response, so monitor and add capacity at 70% sustained load.

### 7.4 Comparison with Alternative Paths (3-year view)

| Option | 3-yr cost (est.) | Meets context/functionality need | CUI control | Comment |
|---|---|---|---|---|
| Continue status quo | $[license] | No | Existing | Capability gap persists; shadow-AI risk |
| Upgrade/expand current tools | $[quote] | Unknown / unlikely | Existing | Verify whether vendors can raise context, add API, add RAG |
| Government cloud LLM | $0.3M–$2M+ (usage-driven) | Yes | Moderate (contract/boundary dependent) | Costs scale with long-context use; data leaves site |
| **Self-hosted Tier B** | **$0.25M–$0.46M** | **Yes** | **Highest** | Fixed cost; needs operations staff |
| Self-hosted Tier C | $0.66M–$1.15M | Yes (larger models, more users) | Highest | Justify with demonstrated demand |

---

## 8. Use Cases and Target Workflows (build out with stakeholders)

| # | Workflow | Users | Context need | Current tool outcome | Proposed outcome |
|---|---|---|---|---|---|
| 1 | Spec/requirements review and gap analysis | [ ] | 100–300K tokens | Must split; incomplete | Single-pass with citations |
| 2 | Test report and data summarization | [ ] | 50–150K | Truncated | Complete summary, tables extracted |
| 3 | Internal knowledge search (RAG) | [ ] | Retrieval + 8–32K | Not available | Cited answers across repository |
| 4 | Script/code development and review | [ ] | 30–200K | Limited to snippets | Whole-project analysis |
| 5 | Report/procedure drafting to standard templates | [ ] | 16–64K | Generic output | Template-aware, consistent |
| 6 | Batch document classification/extraction | [ ] | Per-document | Manual | Automated overnight |
| 7 | Proposal/contract support | [ ] | 100K+ | Not feasible | Compliance matrix drafting |
| 8 | Lessons-learned mining | [ ] | RAG | Not feasible | Trend identification |

---

## 9. Multi-User Operation (Business View)

- One shared platform serves the whole organization; each user sees only the documents and conversations they are authorized for.
- **Fair-use quotas** and priority classes keep interactive users responsive while heavy batch jobs run off-peak.
- **Usage dashboards** show adoption and ROI by team, which supports chargeback/showback if desired.
- **Scalable:** capacity can be added in steps (second GPU node) without changing the user experience.

---

## 10. Risks, Constraints and Mitigations

| Risk / Concern | Mitigation |
|---|---|
| Model output errors (hallucination) | Citations, human review of all outputs used in deliverables, policy and training |
| Authorization timeline (ATO) | Early engagement with security office; leverage hardened baselines |
| Staffing for operations | Dedicated owner, vendor support, documented runbooks, training budget |
| Perceived quality gap vs. top commercial models | Pilot with side-by-side evaluation on real tasks; select best open models; use RAG and prompts tuned to workflows |
| Hardware lead times and cost volatility | Early quotes; modular purchasing; consider short-term compliant cloud for pilot data that is non-CUI |
| Adoption lower than planned | Champions program, training, workflow templates, executive sponsorship |
| Model license/provenance | Legal review; restrict to approved, U.S./allied-origin models |
| Over-reliance on AI | Governance policy, acceptable-use rules, periodic audits |

---

## 11. Success Metrics (KPIs)

| Category | Metric | Target (initial) |
|---|---|---|
| Adoption | Weekly active users / licensed users | ≥ 60% by month 6 |
| Productivity | Self-reported + measured hours saved per user/week | ≥ 1.5 hr |
| Quality | User satisfaction (CSAT) | ≥ 4.0 / 5 |
| Performance | p95 time-to-first-token (≤16K prompt) | < 3 s |
| Performance | Streaming speed per user | ≥ 20 tokens/s |
| Capacity | Sustained GPU utilization | 40–70% |
| Reliability | Platform availability | ≥ 99% during duty hours |
| Compliance | Security findings / CUI incidents | 0 open high findings; 0 incidents |
| Capability | Workflows enabled that were impossible with current tools | ≥ 5 within 6 months |

---

## 12. Implementation Plan (Summary)

1. **Months 0–2:** Requirements, user survey, baseline measurements of current tool usage and pain points; vendor quotes; security engagement.
2. **Months 1–3:** Benchmark candidate models on sanitized/representative workloads; side-by-side comparison against Tool A/B.
3. **Months 2–6:** Procurement, ATO documentation, facility preparation.
4. **Months 5–8:** Deploy Tier B, integrate IdP/logging/RAG, onboard pilot group (20–50 users).
5. **Months 8–12:** Expand, add workflows, measure KPIs, decide on expansion (second node/Tier C).

*(Timeline depends on hardware lead time and authorization pace; not a commitment.)*

---

## 13. Baseline Data to Collect Now (Strengthens the Final Case)

1. Number of users and teams who would use the system; roles and labor rates.
2. Usage statistics and satisfaction for Tool A and Tool B (logins, queries, abandonment).
3. Documented examples where context limits or functionality blocked a task (document sizes, outcomes, time lost).
4. A time study of 5–10 representative tasks done manually vs. with an LLM.
5. License/subscription and support cost of Tool A and B, and contract end dates (potential offset).
6. Any known or suspected instances of unapproved AI tool usage (anonymous survey).
7. Volume of document repositories to be indexed (count, size, formats).
8. Leadership priorities and mission outcomes tied to faster document/engineering throughput.

## 14. Recommendation

Proceed with a benchmark/proof-of-concept and procurement planning for a **self-hosted, CUI-authorized LLM platform starting at Tier B**, with a path to Tier C. The investment is justified by (1) workflows that the current tools cannot perform because of context and functionality limits, (2) controlled handling of CUI, (3) predictable cost versus usage-based cloud pricing, and (4) a reusable internal AI platform. Final funding approval should be conditional on pilot results confirming user demand and measured time savings.

## 15. Approvals

| Role | Name | Decision | Date |
|---|---|---|---|
| Program/Department Sponsor | | | |
| IT / CISO / ISSM | | | |
| Finance | | | |
| Legal / Contracts | | | |
