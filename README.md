

I reviewed the UAIS support response. They confirmed that **Service Principal + Entra ID/RBAC** is the approved authentication approach for Azure AI Search.

The main item we still need to close is the **write/ingestion path**. Since our application will run on AKS, we should update the existing UAIS/Search ticket and ask them to confirm:

1. **Can AKS directly write to Azure AI Search** using the approved Service Principal/Managed Identity, RBAC and private connectivity?
2. If not, **is AML/Databricks the mandatory ingestion path**, with AKS only receiving read/query access?
3. For the required JIT access, please provide:
   - Exact **JIT group name**
   - Who **owns/provisions the JIT group**
   - Which identity should be added — Service Principal / AKS Managed Identity
   - Who is responsible for **assigning the Azure AI Search RBAC roles to that JIT group**
   - Which roles are approved for our use case
   - Exact access-request/JIT process our team needs to follow
Please provide the approved AML/Databricks ingestion implementation or documentation for Azure AI Search writes. We need to understand which AML workspace/compute/pipeline should be used, which identity performs the Search write, and how our Document Intelligence output, chunks, embeddings and metadata should be passed into that process. Please also confirm whether an existing reusable ingestion component is available or whether our team is expected to develop and deploy this pipeline.


Once UAIS confirms the above, **our action** will be to submit the required JIT/access request for the identified runtime identity. The appropriate IAM/platform/resource-owner team can then provision the access and RBAC based on the approved process.

After access is available, we can validate index creation, document/vector ingestion and query access, and then use the same approved connectivity pattern from AKS.

This should give us a clear owner and next action for each dependency rather than assuming who needs to grant the access.
