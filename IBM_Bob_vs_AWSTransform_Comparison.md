# IBM Bob vs AWS Transform — Comparison Table

> **Programme:** HCM EnQuest Mainframe Modernisation | **Prepared by:** Capgemini & IBM | **Date:** 2025–2026
> **Company Confidential** — © Capgemini 2025–2026. All rights reserved.

---

## About AWS Transform

AWS Transform is an agentic AI-powered service designed to accelerate the modernisation of enterprise
workloads, including .NET, Mainframe, and VMware applications. It leverages 19 years of AWS migration
expertise to automate complex tasks — code analysis, dependency mapping, refactoring, and transformation
planning — enabling organisations to modernise at scale while reducing costs and timelines.

Key capabilities:
- Modernise workloads up to **4× faster** than manual approaches
- Support **hundreds of applications in parallel**
- Specialised AI agents per workload type (.NET, Mainframe, VMware)
- Shared workspaces and natural language chat for cross-functional collaboration
- Reduce Windows licensing costs by up to **40%** for .NET applications

---

## Comparison Table

| Dimension | IBM Bob | AWS Transform |
|---|---|---|
| **Deployment Architecture** | Fully on-premises, private cloud, or hybrid — zero external SaaS dependency | AWS-hosted only; all transformation jobs run on AWS infrastructure — no on-prem option |
| **Code Confidentiality** | Source code never leaves the enterprise network | Source code uploaded to AWS and processed on Amazon infrastructure during transformation |
| **Mainframe Modernisation** | Native COBOL, JCL, VSAM, CICS support via IBM watsonx Code Assistant for Z | Mainframe agent exists — reduces timelines from years to months; specific language depth not publicly documented |
| **Modernisation Scope** | COBOL → Java, monolith → microservices, batch → API, multi-language, multi-platform | .NET Framework → cross-platform .NET, Mainframe modernisation, VMware → Amazon EC2 |
| **Agent Architecture** | Parallel specialised subagents — planner, coder, reviewer running simultaneously | Specialised agents per workload type (.NET, Mainframe, VMware) running in parallel across applications |
| **Business Logic Preservation** | Automated lineage mapping traces every COBOL line through to generated Java | Code analysis and dependency mapping included — depth of logic tracing not independently verified |
| **Collaboration** | Jira/ADO integration, structured programme governance, approval gates per task | Shared workspaces and natural language chat for cross-functional teams in real time |
| **Approval Workflow** | Inline per-task governance gates (e.g. DBA sign-off for schema changes) | Transformation planning and progress tracking — per-task approval gates not documented |
| **Regulatory Evidence** | Generates SOX/GDPR-ready evidence packs automatically from agent action logs | No publicly documented compliance evidence pack generation |
| **Model Ownership** | IBM Granite (Apache 2.0 open-weight) — enterprise owns, hosts, and fine-tunes the model | AWS-managed proprietary agents — no model ownership, visibility, or fine-tuning on enterprise code |
| **Fine-Tuning Capability** | Fine-tune on proprietary COBOL/Java corpora for domain-specific accuracy | Agents trained on 19 years of AWS migration expertise — not customisable to enterprise-specific patterns |
| **Cloud Destination** | Cloud-agnostic — AWS, Azure, GCP, or on-prem as target | AWS only — modernisation output is optimised for AWS services and Amazon EC2 |
| **Cost Predictability** | Pooled RU pricing — fixed monthly cost regardless of code volume | Pricing not publicly listed — billed per engagement/workload; cost structure opaque |
| **Hyperscaler Lock-in** | Zero lock-in — portable across any infrastructure | Deep AWS lock-in — modernised workloads land on AWS; re-platforming to another cloud requires re-work |
| **IBM Mainframe Expertise** | 60+ years of IBM mainframe engineering embedded in the platform | 19 years of AWS migration expertise — strong on cloud landing zone, less proven on deep COBOL semantics |

---

## Clarification: What I Initially Got Wrong

An earlier version of this comparison understated AWS Transform's capabilities. The corrections are:

| Earlier Incorrect Statement | Correction |
|---|---|
| "Java version upgrades only" | AWS Transform also covers .NET, Mainframe, and VMware workloads |
| "No mainframe capability" | It does have a dedicated mainframe modernisation agent |
| "No parallel processing" | Supports hundreds of applications modernised in parallel |
| "No agent framework" | Uses specialised AI agents per workload type |
| "No collaboration features" | Has shared workspaces and natural language chat |

---

## Key Differentiators for EnQuest

### 1. Data Sovereignty
AWS Transform requires your COBOL code to leave your network and be uploaded to AWS.
IBM Bob processes everything inside your own network — code never leaves the perimeter.

### 2. Cloud Destination
AWS Transform modernises workloads **onto AWS only**.
IBM Bob lets EnQuest choose AWS, Azure, GCP, or on-premises as the target — no lock-in.

### 3. IBM Mainframe Depth
IBM Bob is built by the company that **invented** the mainframe.
AWS Transform is built by a cloud vendor with strong migration experience.
For deep COBOL semantics, VSAM file structures, and CICS transaction logic, IBM's native expertise is unmatched.

### 4. Model Control
IBM Bob uses open-weight IBM Granite which EnQuest can **fine-tune on its own COBOL codebase**,
improving accuracy on EnQuest-specific code patterns over time.
AWS Transform uses fixed proprietary agents that cannot be customised to enterprise-specific patterns.

---

## Summary

**IBM Bob** is the stronger fit for EnQuest when:
- Strict data-residency / air-gap deployment is required
- Cloud-agnostic or multi-cloud target architecture is needed
- Deep COBOL / JCL / VSAM / CICS comprehension is critical
- Model fine-tuning on proprietary code is required
- SOX / GDPR compliance evidence packs are mandatory

**AWS Transform** is worth considering when:
- EnQuest is committed to AWS as the sole cloud destination
- .NET or VMware modernisation is also in scope alongside mainframe
- AWS migration expertise and toolchain integration are valued
- Data-residency requirements can be met via AWS UK region (eu-west-2)

---

*Data accurate as of May 2025. AWS Transform capabilities sourced from AWS official documentation.
Verify latest pricing and features at aws.amazon.com/transform before board submission.*
