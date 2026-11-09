Hi Sri Ramya,

I reviewed the response from the UAIS support team. At a high level, they confirmed that **Service Principal + Entra ID/RBAC is the approved authentication approach for Azure AI Search**, so our current authentication direction is valid.

The main point we still need to clarify is the **write/ingestion path**. The support guidance mentions that Azure AI Search write operations are currently expected to happen through the approved UAIS AML/Databricks path, while read/query operations can be performed outside UAIS. Since our application will ultimately run in AKS, we need confirmation on whether AKS can directly create/manage the Search index and upload document chunks/embeddings using the approved identity and private connectivity, or whether ingestion must go through AML/Databricks and AKS will only query the index.

They also mentioned that the required Search RBAC roles should be assigned through an approved **JIT group**, rather than directly to a user or Service Principal. My understanding is that the JIT group is the controlled access group used by the platform team to grant the required Azure permissions. The Search roles would be associated with that approved group at the Azure AI Search resource/IAM level through the internal access process.

So the next steps would be:

1. Confirm with UAIS whether **AKS is allowed to perform Search write/ingestion operations**, or if AML/Databricks is mandatory for writes.
2. Identify the **approved JIT group/request process** for Azure AI Search.
3. Request the required Search permissions through that process.
4. Once access is provisioned, test index creation, document/vector upload, and query access before integrating it into the AKS application.

Once we get confirmation on the first two items, we should have a clear path to move the Azure AI Search integration forward.

Thanks,  
Sadanand
