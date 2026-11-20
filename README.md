

AKS → Azure AI Search	Yes	Query medical evidence for Summary/Q&A
AKS → PostgreSQL	Yes	Case data, status, structured data, workflow state
AML → Azure AI Search	Yes	Write/index processed medical data
AML → PostgreSQL	Maybe	Only if AML needs to update processing status
AKS → AML Workspace	Only if AKS triggers AML jobs	Submit/check ingestion job
AKS → Databricks	No	Databricks is not being used
