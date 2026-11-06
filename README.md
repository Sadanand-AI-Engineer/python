We are evaluating **Azure PostgreSQL Flexible Server + pgvector** as an alternative vector store for the UW AI Assistant.

Planned flow:  
**Medical Records → Document Intelligence → Extracted text → Chunking/Embedding → PostgreSQL pgvector → Agent/RAG**

| Area | What we need / confirm |
|---|---|
| **PostgreSQL Setup** | Azure PostgreSQL Flexible Server with **pgvector (`vector`) extension enabled** |
| **Development Access** | Developers should be able to connect from the approved local/VS Code development environment for development and testing |
| **Schema Control** | We need appropriate access to create/manage our application **schema, tables, vector indexes and required DB objects** without requiring full PostgreSQL server-admin access |
| **Data Ingestion** | We need to insert/update extracted medical-record chunks, embeddings and metadata such as member/case/document/page/source information |
| **Query Access** | Need ability to perform metadata-filtered vector similarity searches for RAG |
| **Authentication** | Please confirm the approved authentication approach — **Entra/Managed Identity, Service Principal, or other approved method** |
| **Permissions** | Please confirm which database roles/permissions are required for schema creation, ingestion, updates and querying |
| **Connection Details** | Need PostgreSQL hostname, port, database/schema details and any required connection configuration |
| **Networking** | Need approved private connectivity for development and, later, a supported private path for the application running in **AKS** to access PostgreSQL |
| **Secrets** | Prefer passwordless authentication; if credentials are required, please confirm the approved secret-management approach |
| **Environments** | Please confirm the expected DEV/QA/PROD setup and access separation |

**Main ask:**  
Can PostgreSQL + pgvector be provisioned so our team can develop against it, create/manage the required application DB objects, ingest medical text + embeddings + metadata, perform vector retrieval, and later connect to the same service securely from AKS?
