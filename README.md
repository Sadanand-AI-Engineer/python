Foundry Production Readiness: Internal UAIS/HCP documentation shows Foundry production-readiness guidance, but the team clarified that the enterprise production pattern is still evolving, particularly around security controls, firewall, ingress/egress and critical application requirements.
Platform Options: Two paths were discussed:
Option A: Continue with Microsoft Foundry and validate whether it can meet all production requirements.
Option B: Use a pro-code approach with LangGraph + AKS, without depending on Foundry production readiness.
AKS Infrastructure: For Option B, the team can provision its own Azure infrastructure using existing Dojo360 Terraform modules (Infrastructure as Code). An infrastructure/SRE resource may be required to support provisioning and networking.
UAIS Managed Option: United AI Studio managed AKS/subscription was also discussed as a possible way to use the pro-code approach without the project team managing all infrastructure themselves.
P1 / Resiliency: The overall application is P1, but the team needs to confirm whether the AI capability itself must meet P1 requirements. If yes, the architecture needs multi-region resiliency, with active-active vs. active-passive and DR requirements defined.
Networking & Security: Enterprise networking is deny-by-default. Required ingress/egress paths need firewall approval. Since users are internal underwriters using MSID, private connectivity/private IP was suggested instead of public exposure.
Supporting Services: The discussion mentioned Optum AI Gateway for model access, Cosmos DB for session/state recovery, and AI Patrol + OpenTelemetry for agent observability and evaluation.
Governance: Regardless of Foundry or AKS, production must go through applicable AI Catalog registration, data usage rights, AIRB, security and architecture reviews.
Internal Reference: Other UHG/UHC teams have implemented pro-code Azure agent architectures without Foundry, which can be reviewed for reusable production patterns.
Timeline: Development is targeted during 2026, with potential production deployment around February 2027 after AEP.
Next Step: Document the P1/SLA, resiliency, security, networking, PHI/data, DR, timeline and resource requirements, then compare Foundry vs. AKS/Terraform against those requirements before finalizing the platform.
