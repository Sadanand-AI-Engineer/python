I reviewed the UAIS support response. They confirmed that **Service Principal + Entra ID/RBAC** is the approved authentication approach for Azure AI Search.

The main item we still need to close is the **write/ingestion path**.

The support guidance says Search write operations may be restricted to the approved UAIS AML/Databricks path, while read/query operations can be performed outside UAIS. Since our application will ultimately run in AKS, we need the UAIS/Search team to confirm the supported pattern.

I suggest we reply on the existing ticket and ask them to confirm one of the below:

1. **If AKS can write directly to Azure AI Search**
   - Which Service Principal/Managed Identity should AKS use?
   - Which JIT group should be requested?
   - Which Search RBAC roles should be assigned?
   - What private endpoint/VNet connectivity is required?

2. **If AKS cannot perform write operations**
   - Please provide the approved AML/Databricks ingestion pattern for creating the index and uploading document chunks/embeddings.
   - Confirm whether AKS will then only require read/query access to Azure AI Search.

For the JIT access, we should also ask the support team to provide the **exact JIT group name or access-request path**. Once identified, the required Search roles can be associated with that approved group at the Azure AI Search resource level through the standard access process.

So the immediate next step would be to update the current UAIS ticket with the above questions. Once they confirm the supported write path and JIT group, we can raise the required access/network requests and proceed with integration testing.

