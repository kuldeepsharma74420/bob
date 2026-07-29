# IBM Bob vs GitHub Copilot — Comparison Table

> **Programme:** HCM EnQuest Mainframe Modernisation | **Prepared by:** Capgemini & IBM | **Date:** 2025–2026
> **Company Confidential** — © Capgemini 2025–2026. All rights reserved.

---

| Dimension | IBM Bob | GitHub Copilot |
|---|---|---|
| **Deployment Architecture** | Fully on-premises, private cloud, or hybrid — zero external SaaS dependency | Cloud-only; all inference runs on Microsoft Azure regardless of GitHub Enterprise Server setup |
| **Code Confidentiality** | Prompts, code context, and completions never leave the enterprise network | Code context sent to Azure OpenAI endpoints; content exclusions reduce but do not eliminate egress |
| **Mainframe DNA** | Built on IBM's 60+ years of mainframe engineering; CICS, JCL, VSAM understood natively | No mainframe lineage; COBOL has no dedicated agent or parser support |
| **Agent Concurrency** | Multiple specialised subagents run in parallel — planner, coder, reviewer simultaneously | Single agent per Copilot Workspace session; tasks execute sequentially |
| **Model Ownership** | IBM Granite (Apache 2.0 open-weight) — enterprise can own, host, and fine-tune the model | No model ownership; dependent on Microsoft/OpenAI, Anthropic, and Google model availability |
| **Fine-Tuning Capability** | Fine-tune on proprietary COBOL/Java corpora for domain-specific accuracy | No fine-tuning on custom enterprise code; model behaviour controlled by GitHub/Microsoft |
| **Approval Workflow** | Per-task-type human approval gates enforced inline (e.g. DBA sign-off for schema changes) | No in-session approval workflow; governance enforced at GitHub Actions level, outside the AI session |
| **Regulatory Evidence** | Generates SOX/GDPR-ready evidence packs automatically from agent action logs | Audit log streaming available but does not produce compliance evidence packs |
| **Business Logic Preservation** | Automated lineage mapping ensures COBOL business logic survives transformation | No lineage analysis capability; logic correctness depends entirely on developer review |
| **Multi-Cloud Portability** | Vendor-neutral — deploys identically on AWS, Azure, GCP, or bare-metal | Tied to GitHub.com and Azure infrastructure; portability outside Microsoft ecosystem is limited |
| **Cost Predictability** | Pooled RU pricing absorbs usage spikes — no surprise bills from agentic sessions | Token-based billing for agentic sessions from June 2026 — analyst estimates 10–50× cost rise for heavy Workspace users |
| **IDE Independence** | VS Code, IntelliJ, Eclipse, and mainframe IDEs (IBM Developer for z/OS) all supported | VS Code and JetBrains only; no mainframe IDE support |
| **Organisational Rollout** | Programme-level governance, Jira/ADO integration, and structured onboarding built in from day one | Individual-first self-service signup; enterprise controls added via GitHub org admin after adoption |
| **Hyperscaler Lock-in** | Zero lock-in — model, infrastructure, and workflow fully portable | Microsoft/GitHub lock-in; deep dependency on GitHub.com, Azure OpenAI, and Copilot API surface |

---

## What "On-Premises Deployment" Means for IBM Bob

IBM Bob can run **entirely inside your own data centre or private network**. Nothing is sent to IBM's cloud or any external server.

### How It Works

IBM Granite and Mistral are **open-weight models** — IBM provides the actual model files which you install and run on your own servers. All AI inference happens **inside your network**.

### What Never Leaves Your Network
- Your COBOL source code
- Your prompts and questions to the AI
- The AI's responses and generated code
- Your business logic and proprietary data

### Three Deployment Options for EnQuest

| Option | What It Means |
|---|---|
| **On-Premises** | Bob runs on EnQuest's own physical servers in your data centre. Nothing goes to the internet. |
| **Private Cloud** | Bob runs on a dedicated cloud environment (e.g. IBM Cloud, AWS VPC) accessible only to EnQuest. |
| **Hybrid** | Sensitive COBOL code stays on-prem; less sensitive workloads run in a private cloud. |

### Why This Matters for EnQuest

EnQuest handles **oil & gas operational data** subject to strict UK data-residency and confidentiality rules. COBOL source code containing pricing logic, reservoir models, or financial calculations **cannot leave your network** under many enterprise agreements.

- **GitHub Copilot** — always sends code to Microsoft Azure. ❌
- **Amazon Q Developer** — always sends code to Amazon Bedrock. ❌
- **IBM Bob** — runs 100% inside your perimeter. ✅

---

## Summary

**IBM Bob** is the superior fit for EnQuest requiring:
- Air-gapped / data-sovereign deployments
- Native COBOL / JCL / VSAM comprehension
- SOX / GDPR compliance audit trails
- Parallel agentic workstreams at programme scale
- Model ownership and fine-tuning on proprietary code

**GitHub Copilot** is best suited for:
- Greenfield cloud-native Java / TypeScript development
- Individual contributor velocity on GitHub-hosted repos
- Teams already in the Microsoft / GitHub ecosystem
- Low-friction rollout with zero infrastructure setup

---

*Data accurate as of May 2025. Verify latest pricing and features before board submission.*
