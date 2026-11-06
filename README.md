We are using Azure AI Search for the UW AI Assistant RAG flow:

Document Intelligence → Chunking → Embedding Model → Azure AI Search → Foundry Hosted Agent.

We need to create/manage an Azure AI Search index and upload the extracted document chunks, embeddings, and metadata into the index. The Hosted Agent will then query this index for RAG.

Please provide/confirm the approved connection and authentication details:
- Azure AI Search endpoint
- Search service/index details
- Approved authentication method — Managed Identity / Service Principal / other approved identity
- If Service Principal is used: Tenant ID and Client/Application ID (secret should be managed through the approved secret-management process)
- If key-based authentication is supported, please confirm how the Search API key should be obtained/managed.

Please also confirm whether assigning the following RBAC roles to the approved runtime identity will enable this flow:
- **Search Service Contributor** – create/manage indexes
- **Search Index Data Contributor** – upload/update/delete documents and embeddings
- **Search Index Data Reader** – query/retrieve indexed content

If direct contributor access is not permitted, please provide the approved identity/service and process teams normally use to create the index and ingest documents into Azure AI Search.
