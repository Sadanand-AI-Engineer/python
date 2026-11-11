AKS setup: “For this workload, do we get a dedicated AKS cluster or a namespace in an existing enterprise cluster? What exactly will your team provision for us?”

DEV/QA/PROD: “Are DEV, QA and PROD separate clusters, or separate namespaces in the same cluster? How are identities, network access and configuration separated between them?”

Node pools: “Do you recommend one user node pool for our FastAPI/LangGraph workloads, or should batch ingestion/background workers be on a separate node pool?”

Pod design: “Our LangGraph agents are logical agents inside one Python application. Is it okay to deploy them as one AKS service initially, or do you recommend separate deployments for any components?”

Pod-to-pod communication: “If we later separate the orchestrator, ingestion worker and other services into different pods, what is the approved way for them to communicate internally—ClusterIP/service DNS, internal ingress, or something else?”

Pod failure: “If one pod crashes while processing a case, how will the request/job recover? Should we design the workflow to resume from PostgreSQL/checkpoints instead of relying on pod memory?”

Node failure: “If the node hosting our pod fails, will Kubernetes automatically reschedule it on another node, and what replica count/PDB/readiness/liveness settings do you require for production?” AKS recommends multiple replicas, health probes and Pod Disruption Budgets for production reliability. Microsoft Learn

Scaling: “How should we scale this application—HPA based on CPU/memory, request count, queue depth, or another metric? And is cluster autoscaling already enabled?”

Long-running medical ingestion: “Some medical-record processing can take a long time. We don't want an API request tied to a pod for 30–60 minutes. What background-job/queue pattern is approved in this AKS platform?”

Ingress from Salesforce: “What is the approved path for Salesforce/ASCRM to call our AKS API—APIM, Application Gateway, internal load balancer, enterprise ingress, or something already provided by the platform?”

Outbound connectivity: “Our pods need to call several endpoints—MuleSoft/internal APIs, PostgreSQL, Azure AI Search, GPT/UAG, Key Vault, and possibly Document Intelligence. Do we need to submit every outbound hostname/port for firewall or egress approval?”

Private networking: “For Azure AI Search and PostgreSQL, what private endpoint/VNet/DNS setup will be required from AKS? Which team creates the private endpoint and DNS records?” AKS production guidance recommends private/internal exposure where possible and network policies to restrict traffic. Microsoft Learn

AML/Databricks path: “Since Azure AI Search writes must run through approved AML/Databricks, how should AKS hand off the extracted medical data to that ingestion process? Do we call an AML job/API, trigger Databricks, or drop data into an approved staging location?”

Search read from AKS: “For AKS querying Azure AI Search, do you want us to use AKS Workload Identity/Managed Identity, or the Service Principal pattern UAIS described?”

Workload identities: “Can we have separate Kubernetes service accounts/workload identities for components that need different permissions—for example Search read, PostgreSQL write, and Key Vault access—or is one application identity standard here?”

Tool security: “Our LangGraph code restricts which tools each agent can call. From the infrastructure side, can we also restrict the workload identity so the application only has access to the specific APIs/resources it needs?”

Key Vault: “How should the pods consume secrets from Key Vault? Do you support Workload Identity + Key Vault CSI/SDK, and do we need any secrets stored as Kubernetes Secrets?”

PostgreSQL: “Once PostgreSQL Flexible Server is provisioned, what is the approved AKS connectivity/authentication pattern? Can the pod use Entra/Managed Identity, and who creates the database roles for SELECT/INSERT/UPDATE/schema access?”

Connection pooling: “Since multiple pods may open PostgreSQL connections, do we need PgBouncer or another connection pool? Are there platform standards or max-connection limits we need to design around?”

Container registry: “Which ACR should we use? Will AKS already have pull access, and does the image have to pass any vulnerability/security scan before deployment?”

CI/CD: “Our source will be GitHub. What is the approved pipeline from GitHub → build → ACR → Helm → AKS? Are there existing enterprise templates we are required to use?”

Deployment/rollback: “For a new agent release, do you support rolling deployment, blue/green or canary? If the deployment fails, what is the standard rollback process?”

Configuration: “Can we keep the exact same Docker image across DEV/QA/PROD and inject only environment-specific endpoints, identities and configuration at deployment time?”

Network policies: “Do you require Kubernetes NetworkPolicies between namespaces/pods? For example, can we explicitly allow our API pod to call PostgreSQL/Search while preventing unrelated workloads from reaching it?”

Observability: “For infrastructure, what monitoring do we get by default for node health, pod restarts, CPU/memory, request latency and failures? Is Container Insights/Prometheus already enabled?” Microsoft specifically recommends Container Insights and production monitoring for AKS. Microsoft Learn

AI Patrol: “For agent-level observability, we plan to send LangGraph/tool/LLM traces to AI Patrol. What collector/OTel endpoint should the AKS pods use, and do you already provide a sidecar/agent or do we instrument the Python app ourselves?”

PHI/logging: “Because this is underwriting/medical data, what data are we allowed to put into application logs and traces? Do you provide any logging/redaction standards we need to follow?”

Availability zones: “For production, will this AKS cluster be zone-redundant? We need to know this before creation because availability-zone choices are made at cluster/node-pool design time.” Microsoft recommends availability zones for production resilience. Microsoft Learn

DR: “If the AKS region goes down, what is our recovery model? Is there another AKS cluster/region, and how are ACR, PostgreSQL, Search and configuration handled during failover?”

Ownership/support: “After production goes live, which team owns cluster upgrades, Kubernetes version upgrades, node OS patches, certificate rotation, scaling issues and production incidents—and what remains with our application team?”
