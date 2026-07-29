# IBM Bob vs Amazon Q Developer — Comparison Table

> **Programme:** HCM EnQuest Mainframe Modernisation | **Prepared by:** Capgemini & IBM | **Date:** 2025–2026
> **Company Confidential** — © Capgemini 2025–2026. All rights reserved.

---

| Dimension | IBM Bob | Amazon Q Developer |
|---|---|---|
| **Deployment Architecture** | Runs fully on-premises, private cloud, or hybrid — zero dependency on external SaaS | SaaS-only; runs on AWS infrastructure regardless of PrivateLink configuration |
| **Code Confidentiality** | Prompts, code context, and completions never leave the enterprise network | Code context transmitted to Amazon Bedrock endpoints for inference |
| **Mainframe DNA** | Built on IBM's 60+ years of mainframe engineering; understands CICS, JCL, VSAM natively | No mainframe lineage; treats COBOL as an unsupported legacy language |
| **Agent Concurrency** | Multiple specialised subagents execute in parallel — planner, coder, reviewer simultaneously | Single agent per session; tasks queue sequentially with no parallelism |
| **Model Ownership** | Uses IBM Granite (Apache 2.0 open-weight) — enterprise can own, host, and fine-tune the model | Relies on third-party models via Bedrock (Claude, Llama, Titan) — no model ownership |
| **Fine-Tuning Capability** | Supports fine-tuning on proprietary COBOL/Java corpora for domain-specific accuracy | No fine-tuning on custom enterprise code; model behaviour is fixed by AWS |
| **Approval Workflow** | Per-task-type human approval gates enforced inline (e.g. DBA sign-off for schema changes) | No native in-session approval workflow; governance happens outside the AI layer |
| **Regulatory Evidence** | Generates SOX/GDPR-ready evidence packs automatically from agent action logs | CloudTrail logs API calls but does not produce compliance evidence packs |
| **Business Logic Preservation** | Automated lineage mapping ensures COBOL business logic survives transformation | No lineage analysis; logic loss in migration must be caught by manual testing |
| **Multi-Cloud Portability** | Vendor-neutral; deploys identically on AWS, Azure, GCP, or bare-metal | Optimised exclusively for AWS; guidance degrades significantly outside AWS ecosystem |
| **Cost Predictability** | Pooled RU pricing absorbs usage spikes — no surprise bills from agentic sessions | Per-user seat + per-LOC transform billing; high-volume agentic use can spike costs unpredictably |
| **IDE Independence** | Works across VS Code, IntelliJ, Eclipse, and mainframe IDEs (IBM Developer for z/OS) | Primarily VS Code and JetBrains; no mainframe IDE support |
| **Organisational Rollout** | Structured onboarding with programme-level governance built in from day one | Self-service individual signup; enterprise controls bolted on via AWS admin console after the fact |
| **Hyperscaler Lock-in** | Zero lock-in — model, infrastructure, and workflow are all portable | Deep AWS lock-in; switching away requires replacing the entire AI toolchain |

---

## Summary

**IBM Bob** is the superior fit for enterprise mainframe modernisation programmes requiring:
- Air-gapped / data-sovereign deployments
- Native COBOL / JCL / VSAM comprehension
- SOX / GDPR compliance audit trails
- Parallel agentic workstreams at programme scale
- Model ownership and fine-tuning on proprietary code

**Amazon Q Developer** is best suited for:
- Greenfield AWS-native microservice development
- Java version upgrade automation (8/11 → 17/21)
- Teams deeply invested in the AWS ecosystem
- Low-cost evaluation via generous free tier

---

*Data accurate as of May 2025. Verify latest pricing and features before board submission.*
