I’ve been reviewing this from the production architecture side as well. For an agentic workload like the Underwriting AI Assistant, I think the platform decision can be evaluated against these areas:

Agent runtime/orchestration: If Foundry Agent Service supports our required multi-agent orchestration, tool calling, scaling and versioning in production, we can use the managed Foundry runtime; if we need deeper runtime/container control, AKS + ACR would be the alternative.
Enterprise integration: If Foundry agents can securely consume our approved enterprise APIs, use Foundry tools/connections → APIM/MuleSoft; keep Azure AI Search for unstructured RAG. If direct agent integrations are restricted, put the integrations behind our own API/tool layer.
Identity & authorization: Prefer Entra ID/OAuth2 for Salesforce/API access and Managed Identity + RBAC for Azure resources. If a target system does not support Managed Identity, use its approved OAuth/service-principal mechanism with credentials in Key Vault.
Network isolation: If Foundry supports the required private endpoint/VNet connectivity across Search, Storage, Key Vault, model and enterprise API paths, use Foundry; if the runtime/network controls are insufficient, AKS with private networking and controlled egress gives us more control.
Guardrails/governance: Use Foundry guardrails/Content Safety where they satisfy requirements, while keeping application-level PHI/PII, member authorization, tool allowlists, grounding/citation and no-decision controls where platform guardrails are insufficient.
Evaluation/observability: Prefer Foundry Evaluations + Application Insights/OpenTelemetry if they meet UHG monitoring requirements; if UHG requires AI Patrol/Arize or another enterprise observability platform, export the required agent/model/tool telemetry there.
Release/rollback: If Foundry provides the required agent/model/prompt versioning and rollback controls, use its managed lifecycle; otherwise manage releases through Git + CI/CD + ACR/AKS, promoting the same tested artifact through DEV → QA → PROD.

Suggestion: I would evaluate Foundry first if it is UHG-supported, then specifically validate private networking, enterprise integrations, governance/PHI controls, observability and release/rollback requirements. If any of those require greater infrastructure/runtime control than Foundry provides, AKS/ACR is a strong alternative for the agent runtime while retaining Azure AI Search and the approved model/API services.

# python
