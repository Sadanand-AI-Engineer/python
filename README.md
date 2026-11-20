

I had a discussion with Shubham today regarding how our data can be brought into and consumed within the UAIS setup. Below are the key takeaways and the steps we need to work through.

**1. AML/UAIS setup**
- For our use case, AML Workspace is mainly being used to access the underlying UAIS-provisioned resources such as storage and compute.
- There is default storage associated with AML, along with storage created through the different UAIS data connectors.
- Ingress connector storage is generally read-only from inside the workspace. Data is written into it only through the connector workflow.
- Egress connector storage supports taking data out and can be read/write depending on the connector.

**2. Available data-ingestion options**
Shubham mentioned the following supported connector patterns:
- Ad-hoc connector – for on-demand/file upload scenarios.
- On-prem database connector – for sources such as SQL Server, PostgreSQL, MySQL and Oracle.
- ECG ingress/egress – SFTP/flat-file-based automated data movement between source and destination.
- Snowflake connector – for Snowflake data sources.

The exact connector needs to be selected based on our source, data format and required refresh frequency.

**3. Direct API connectivity is the main challenge**
Our requirement includes MuleSoft APIs, DocDNA and other API endpoints. Shubham clarified that UAIS does not have a standard data connector that directly exposes arbitrary APIs.

Direct API access can still be requested through firewall allow-listing, but since we have multiple endpoints, each request will go through enterprise networking/security review and may require significant governance approvals.

He also mentioned that direct access to some DMZ/Core locations may not be permitted based on existing enterprise policies.

**4. Alternative approach suggested**
If opening all the direct API connections becomes difficult, one option he has seen other teams use is:

External instance/database outside UAIS  
→ connect to required APIs and collate the required data  
→ use a supported UAIS data connector  
→ bring the consolidated data into UAIS  
→ AML/AKS consumes it from there.

He was clear that this is only one possible approach, not a mandated solution. We need to evaluate whether this works for our real-time requirements.

**5. Data governance is the first mandatory step**
Before finalizing the connectivity approach, the required data governance approval needs to be completed.

The process discussed was:
- If the required data is already available as a registered Data Product, use the Data Catalog subscription workflow, where the DUR process is integrated.
- If it is not available as a Data Product, submit a new DUR through EGRC.
- For our current case, we discussed proceeding through the EGRC DUR route.
- Once approved, the DUR can be referenced in UAIS for record-keeping. Adding the DUR in UAIS itself does not enable any technical connectivity.

**6. Recommended next steps**
1. Start the EGRC DUR/data-governance approval.
2. Review the UAIS data-connector documentation already shared by Shubham.
3. List each of our sources — MuleSoft APIs, DocDNA, PCH, Salesforce, etc. — and identify:
   - whether real-time access is mandatory,
   - whether batch/periodic refresh is acceptable,
   - whether an existing connector can support it.
4. Use the existing UAIS connectors wherever the business latency allows.
5. For sources that genuinely require on-demand API access, submit the specific firewall allow-listing request through UAIS so they can forward it to the enterprise networking/security team.
6. If direct API approvals become a blocker, evaluate the external staging/database approach suggested by Shubham and bring the consolidated data into UAIS using a supported connector.

The main point from the discussion is that we first need to complete the governance approval and then decide source-by-source whether we can use an existing UAIS connector or need to pursue direct API connectivity.






based on this discussion with shobhan, i need to send takeaways to my lead sri ramya , so draft email, not high lebel, but clear stp by step, ( goal is this is what happened , these are the steps, we have , but detailed step, write in human tone ), but do not hallicuinate write on based on recent discussion


here is coversation:


mail should be clear and not too log and easy to understand

Thanks,  
Sadanand
