# Business Justification: Self-Hosted Enterprise LLM Platform vs. Current In-House AI Tools

| Field | Value |
|---|---|
| Document status | DRAFT v0.2 – revised for a $15K–$55K hardware budget; base material for a future formal report |
| Date | 2026-10-16 |
| Prepared for | [Sponsor / Decision Authority] |
| Prepared by | [Author] |
| Companion document | `01_Analysis_of_Alternatives_CUI_LLM_Platform.md` |
| Supersedes | v0.1 (archived in `archive_v1_large_budget/`) |

> **Note.** Figures marked *illustrative* are placeholders that demonstrate the calculation method. Replace them with measured values (users, hours, labor rate, license cost) before using this document to request funding. Items in `[brackets]` need input.

---

## 1. Purpose

Justify investment in a dedicated, on-premises LLM platform authorized for CUI, compared with continued reliance on the two AI tools currently provided by [Organization] ("Tool A" and "Tool B").

## 2. Executive Summary

- The current tools are **functionally limited and constrained by small context windows**, so they cannot support the document-heavy, multi-step engineering workflows the organization needs (long specs, multi-document comparison, large scripts/codebases, report generation).
- Staff either work around the limits manually, abandon the tools, or are tempted to use unapproved external tools, which is a CUI spill risk.
- A self-hosted platform provides **≥128K context**, an **API for automation**, **RAG over internal repositories**, **multi-user concurrency**, and **full control of CUI** inside the existing authorization boundary.
- **Investment (recommended Tier 3):** about **$35K hardware** (range $33–40K), **$15–35K one-time integration/authorization effort** (mostly internal labor), and roughly **$5–9K/yr** non-labor operating cost plus **0.25–0.5 FTE** operations time. The platform can grow to ~$55K (Tier 5) by adding GPUs.
- *Illustrative* result: payback in **~3 months** in the expected case (60 active users saving 2 hr/week) and **~21 months** in the conservative case (Section 7).
- The strongest justification is not only cost: it is **enabling workflows that are impossible today** and **reducing data-handling risk**.

---

## 3. Current State

### 3.1 Existing Tools (complete the table)

| Attribute | Tool A: [name] | Tool B: [name] | Needed for target workflows |
|---|---|---|---|
| Hosting / owner | [ ] | [ ] | On-prem or accredited enclave |
| CUI authorized? | [ ] | [ ] | Yes (required) |
| Underlying model | [ ] | [ ] | Selectable, upgradable, auditable |
| Max context window | [e.g., 4K–32K] | [ ] | ≥128K |
| Max output length | [ ] | [ ] | ≥4K–8K tokens |
| File/document upload limits | [ ] | [ ] | Large PDFs, spreadsheets, code |
| API / automation | [ ] | [ ] | Yes (OpenAI-compatible) |
| RAG over internal data | [ ] | [ ] | Yes, with per-group access control |
| Concurrency / rate limits | [ ] | [ ] | Supports team-wide peak use |
| Customization | [ ] | [ ] | Prompt libraries, custom tools, optional LoRA |
| Code/script assistance quality | [ ] | [ ] | Strong |
| Audit logging | [ ] | [ ] | Per-user, exportable to SIEM |
| Cost model | [ ] | [ ] | Predictable |
| Roadmap control | Vendor | Vendor | Organization-controlled |
| Retention / training on inputs | [ ] | [ ] | None; org-controlled |

### 3.2 Observed Pain Points (validate with user survey)
1. **Context limits** force document splitting, losing cross-references and giving inconsistent answers.
2. **Limited functionality:** weak file handling, no custom tools, no API or workflow chaining.
3. **Quality gaps** on technical reasoning, code, and long structured output.
4. **Low adoption/trust:** users stop using tools after poor results, so existing spend yields little value.
5. **Shadow-AI risk:** users may paste work content into unapproved tools.
6. **No adaptability** to organizational terminology, templates and standards.

---

## 4. Proposed Solution (Summary)

An on-premises GPU server running open-weight LLMs (e.g., a ~120B-class mixture-of-experts model), with chat UI, OpenAI-compatible API, RAG over controlled repositories, SSO/MFA and full audit logging, all inside the CUI boundary. Recommended purchase: **Tier 3 (~$35K)**: two 96 GB GPUs in a 4-GPU-capable chassis with a separate app/data server, backup and UPS. It supports roughly **8–20 simultaneous active users** (30–100 named users) at 128K context, and grows to **Tier 5 (~$55K, 25–50 active users)** by adding GPUs at ~$9K each. See the AoA for details.

| Tier | Hardware | Named users | Simultaneous active |
|---|---|---|---|
| 1 (~$15K) pilot | 1 GPU | 10–30 | 3–8 |
| 2 (~$25K) | 2 GPUs | 25–75 | 8–20 |
| **3 (~$35K) recommended** | 2 GPUs + app tier/backup | 30–100 | 8–20 |
| 4 (~$45K) | 3 GPUs | 50–150 | 15–35 |
| 5 (~$55K) | 4 GPUs | 75–250 | 25–50 |

---

## 5. Benefits

### 5.1 Capability Benefits (what existing tools cannot do)

| Capability | Business value | Example workflow |
|---|---|---|
| **Large context (128K tokens ≈ 300 pages)** | Analyze entire specs/reports in one pass | Compare a 200-page spec to a test report and list gaps |
| **Multi-document RAG with citations** | Find and cite answers across thousands of documents | "What did past programs decide about connector X?" with sources |
| **API access** | Embed the LLM in scripts, pipelines, spreadsheets | Nightly summary of new anomaly reports |
| **Code/script assistance on larger codebases** | Faster development, documentation, test generation | Review a multi-file Python/MATLAB toolchain and generate unit tests |
| **Concurrent multi-user access with quotas** | Team-wide availability and predictable response | 15 engineers using it at once at peak |
| **Batch processing** | Bulk tasks run overnight | Classify/summarize 10,000 legacy records |
| **Customization** | Organization-specific templates, prompts, tools | Draft reports in the standard format |
| **Model choice and upgrades** | Swap in better models as released; no vendor lock-in | Adopt a new approved model within days |
| **Structured output / tool use** | Reliable JSON/forms | Auto-populate traceability matrices |

### 5.2 Productivity Benefits
*Published studies show wide ranges; validate in the pilot.*

| Task category | Baseline effort | Expected reduction |
|---|---|---|
| Document summarization / review | 1–4 hr | 40–70% (largest with long context) |
| First-draft reports, emails, procedures | 1–3 hr | 30–50% |
| Information search across repositories | 0.5–2 hr | 50–80% (needs RAG) |
| Code/script writing, debugging, tests | varies | 20–40% |
| Data extraction/transformation | 1–6 hr | 40–80% |
| Requirements/traceability analysis | 4–16 hr | 30–60% |

### 5.3 Risk-Reduction Benefits
- **CUI containment:** processing stays inside the boundary; no third-party retention or training on inputs.
- **Less shadow AI:** a capable approved tool reduces the incentive to use unapproved ones.
- **Auditability:** per-user logs and retrieval records support compliance evidence.
- **Supply-chain control:** approved, hash-verified model inventory.
- **Continuity:** not dependent on vendor changes to pricing, terms or features.

### 5.4 Strategic Benefits
- Builds in-house AI engineering capability and a reusable platform.
- Makes historical documents searchable and usable.
- Foundation for domain-specific assistants and controlled agentic workflows.

---

## 6. Costs

Recommended **Tier 3**; replace with quotes.

| Cost element | Estimate |
|---|---|
| Hardware (2 × 96 GB GPUs, 4-GPU-capable server, app server, storage/backup, network, UPS) | $33–40K (≈ $35K) |
| Integration, hardening, ATO documentation (one-time; largely internal labor) | $15–35K |
| Software (open-source stack; OS subscription) | $1–3K/yr |
| Support/warranty extension | $1–3K/yr |
| Power and cooling (~1.5–2 kW continuous ≈ 13–17 MWh/yr at $0.10–0.20/kWh) | $1.5–3.5K/yr |
| **Annual non-labor opex** | **$5–9K/yr** |
| Operations/ML engineering (0.25–0.5 FTE at ~$120K loaded) | $30–60K/yr |
| **3-yr TCO excl. labor** | **$63–102K** |
| **3-yr TCO incl. labor** | **$153–282K** |
| Expansion to Tier 4/5 (add 1–2 GPUs) | +$9–10K per GPU |

Costs of the status quo to include (fill in): current license/subscription fees $[ ]/yr, support effort $[ ]/yr, productivity lost to limitations, cost of any CUI incident or rework.

> **Sourcing caveat:** if TAA-compliant OEM hardware is required, hardware cost may be 15–40% higher (roughly $40–50K for Tier 3).

---

## 7. Financial Analysis (Method + Illustrative Example)

### 7.1 Formulas

$$\text{Annual benefit} = N_{\text{active}} \times H \times W \times R \times E$$

$N_{\text{active}}$ = regular active users, $H$ = hours saved per user per week, $W$ = working weeks per year (~46), $R$ = burdened labor rate ($/hr), $E$ = realization factor (fraction of saved time turned into useful work; use 0.5–0.7).

$$\text{ROI} = \frac{\text{3-yr benefit} - \text{3-yr cost}}{\text{3-yr cost}} \qquad \text{Payback (months)} = \frac{\text{Upfront cost}}{\text{Net annual benefit} / 12}$$

### 7.2 Illustrative Scenarios (*all inputs are placeholders*)

| Input | Conservative | Expected | Optimistic |
|---|---|---|---|
| Active users ($N$) | 40 | 60 | 100 |
| Hours saved / user / week ($H$) | 1.0 | 2.0 | 3.0 |
| Working weeks ($W$) | 46 | 46 | 46 |
| Burdened rate ($R$) | $100/hr | $100/hr | $100/hr |
| Realization ($E$) | 0.5 | 0.6 | 0.7 |
| **Annual benefit** | **$92K** | **$331K** | **$966K** |
| Annual run cost (non-labor + labor) | $50K | $50K | $60K |
| Upfront cost (hardware + integration) | $75K (Tier 3, high end) | $60K (Tier 3) | $85K (Tier 5) |
| **Net annual benefit** | **$42K** | **$281K** | **$906K** |
| **Payback** | ~21 months | **~2.6 months** | ~1.1 months |
| **3-yr ROI** | ~23% | **~370%** | ~990% |

> The conservative case returns only modestly on time savings alone, which is why the capability and risk arguments (5.1, 5.3) matter. The optimistic case with 100 active users needs Tier 4–5 capacity and is likely unrealistic as a planning basis. Productivity savings are often not budget-recoverable "cash"; present them as **capacity gained** (more throughput without added headcount) unless a headcount or contract-cost effect can be shown. Run cost uses 0.35 FTE of labor ($42K) plus ~$8K non-labor.

### 7.3 Sensitivity
- **Biggest driver:** hours saved per user per week. In the expected case, each additional 0.5 hr/week across 60 users is worth ≈ **$83K/yr**.
- **Adoption:** benefits scale with *active* users; plan training and champions.
- **Labor:** at this hardware budget, the operations labor share is the largest cost. If labor is unfunded or unassigned, the project is at risk regardless of hardware.
- **Utilization:** monitor GPU load; add a GPU at 70% sustained utilization.

### 7.4 Comparison of Paths (3-year view)

| Option | 3-yr cost (est.) | Meets context/functionality need | CUI control | Comment |
|---|---|---|---|---|
| Continue status quo | $[license] | No | Existing | Capability gap persists; shadow-AI risk |
| Upgrade/expand current tools | $[quote] | Unknown / unlikely | Existing | Ask vendors about context, API and RAG roadmap |
| Government cloud LLM | $0.1M–$0.6M (usage-driven) | Yes | Moderate (contract/boundary dependent) | Cost scales with long-context use; data leaves site |
| Self-hosted Tier 1 (pilot) | $27–47K + labor | Partially (few users) | Highest | Good for proof-of-concept |
| **Self-hosted Tier 3 (recommended)** | **$63–102K + labor** | **Yes** | **Highest** | Production-ready for ~8–20 simultaneous users |
| Self-hosted Tier 5 | $99–143K + labor | Yes (more users, larger models) | Highest | Reached by adding GPUs as demand proves out |

*Break-even vs. cloud depends on usage (see AoA 7.3): roughly 18 months at $4K/month of cloud spend; cloud is cheaper if usage stays light.*

---

## 8. Use Cases and Target Workflows (build out with stakeholders)

| # | Workflow | Users | Context need | Current tool outcome | Proposed outcome |
|---|---|---|---|---|---|
| 1 | Spec/requirements review and gap analysis | [ ] | 100–300K tokens | Must split; incomplete | Single pass with citations |
| 2 | Test report and data summarization | [ ] | 50–150K | Truncated | Complete summary, extracted tables |
| 3 | Internal knowledge search (RAG) | [ ] | Retrieval + 8–32K | Not available | Cited answers across repository |
| 4 | Script/code development and review | [ ] | 30–200K | Limited to snippets | Larger-scope analysis |
| 5 | Report/procedure drafting to templates | [ ] | 16–64K | Generic output | Template-aware, consistent |
| 6 | Batch classification/extraction | [ ] | Per document | Manual | Automated overnight |
| 7 | Proposal/contract support | [ ] | 100K+ | Not feasible | Compliance matrix drafting |
| 8 | Lessons-learned mining | [ ] | RAG | Not feasible | Trend identification |

---

## 9. Multi-User Operation (Business View)

- One shared platform serves the organization; each user sees only the documents and conversations they are authorized for.
- **Fair-use quotas** and priority classes keep interactive users responsive while batch jobs run off-peak.
- **Usage dashboards** show adoption and benefit by team (supports showback/chargeback).
- **Incremental scaling:** capacity grows by adding GPUs (~$9K each) without changing the user experience.
- **Limits to communicate:** at Tier 3, about 8–20 people can be generating at the same moment. Others queue briefly. Very long (128K) requests consume more capacity than short chats.

---

## 10. Risks, Constraints and Mitigations

| Risk / Concern | Mitigation |
|---|---|
| Output errors (hallucination) | Citations, human review of anything used in deliverables, policy and training |
| ATO timeline | Early engagement with security office; hardened baselines |
| Operations staffing | Assign a named owner and time allocation; documented runbooks |
| Quality gap vs. top commercial models | Pilot with side-by-side evaluation on real tasks; use RAG and tuned prompts |
| TAA/OEM sourcing raises hardware cost 15–40% | Confirm early; get OEM quotes |
| No hardware redundancy at this budget | Cold spares, data backups, cloud contingency plan |
| Adoption lower than planned | Champions, training, workflow templates, sponsorship |
| Model license/provenance | Legal review; approved U.S./allied-origin models |
| Over-reliance on AI | Governance policy, acceptable-use rules |

---

## 11. Success Metrics (KPIs)

| Category | Metric | Target (initial) |
|---|---|---|
| Adoption | Weekly active users / named users | ≥ 60% by month 6 |
| Productivity | Hours saved per user per week (survey + measured) | ≥ 1.5 hr |
| Quality | User satisfaction | ≥ 4.0 / 5 |
| Performance | p95 time-to-first-token (≤16K prompt) | < 3 s |
| Performance | Streaming speed per user | ≥ 15–20 tokens/s |
| Capacity | Sustained GPU utilization | 40–70% |
| Reliability | Availability during duty hours | ≥ 98% |
| Compliance | Open high security findings / CUI incidents | 0 / 0 |
| Capability | Workflows enabled that were impossible before | ≥ 5 within 6 months |

---

## 12. Implementation Plan (Summary)

1. **Months 0–2:** requirements, user survey, baseline usage of Tools A/B, sourcing rules, quotes, security engagement.
2. **Months 1–3:** pilot on a Tier 1-class unit (or temporary compliant environment); benchmark candidate models; side-by-side with Tools A/B.
3. **Months 2–6:** procurement, ATO documentation, facility preparation.
4. **Months 5–8:** deploy Tier 3; integrate IdP/logging/RAG; 20–40 pilot users.
5. **Months 8–12:** expand workflows; measure KPIs; add GPUs (Tier 4–5) if triggers are met.

*(Dependent on lead time and authorization pace; not a commitment.)*

---

## 13. Baseline Data to Collect Now

1. Number of prospective users by team; roles and labor rates.
2. Usage statistics and satisfaction for Tool A and B.
3. Documented cases where context limits or missing functionality blocked a task (document sizes, time lost).
4. Time study of 5–10 representative tasks done manually vs. with an LLM.
5. License/support cost of Tool A and B and contract end dates (possible offset).
6. Known or suspected use of unapproved AI tools (anonymous survey).
7. Volume of document repositories to index (count, size, formats).
8. Who will operate the platform and their available time.

## 14. Recommendation

Proceed with a benchmark/pilot and procurement planning for a **self-hosted, CUI-authorized LLM platform at Tier 3 (~$35K hardware)**, built on a 4-GPU-capable chassis so it can grow to Tier 5 (~$55K). The investment is justified by (1) workflows the current tools cannot perform due to context and functionality limits, (2) controlled handling of CUI, (3) a low fixed hardware cost compared with usage-based cloud pricing at heavy use, and (4) a reusable internal AI platform. Funding should be conditional on pilot results that confirm demand and measured time savings, and on a named operations owner.

## 15. Approvals

| Role | Name | Decision | Date |
|---|---|---|---|
| Program/Department Sponsor | | | |
| IT / CISO / ISSM | | | |
| Finance | | | |
| Legal / Contracts | | | |
