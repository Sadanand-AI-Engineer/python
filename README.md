#
# pip install azure-identity azure-search-documents

from azure.identity import ClientSecretCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import (
    SearchIndex,
    SimpleField,
    SearchableField,
    SearchField,
    SearchFieldDataType,
    VectorSearch,
    HnswAlgorithmConfiguration,
    VectorSearchProfile,
)

# --- your values ---
tenant_id     = "db05faca-c82a-4b9d-b9c5-0f64b6755421"   # from the log
client_id     = "<client_id>"
client_secret = "<client_secret>"
endpoint      = "https://ttr6f35cvgdmojt-acss.search.windows.net"
index_name    = "uwassist-test-index"

credential = ClientSecretCredential(tenant_id, client_id, client_secret)
index_client = SearchIndexClient(endpoint=endpoint, credential=credential)

# Schema matches uw-ai-assist's DocumentChunk model
fields = [
    SimpleField(name="chunk_id", type=SearchFieldDataType.String, key=True),
    SimpleField(name="member_id", type=SearchFieldDataType.String, filterable=True),
    SearchableField(name="text", type=SearchFieldDataType.String),
    SimpleField(name="source_system", type=SearchFieldDataType.String, filterable=True),
    SimpleField(name="event_date", type=SearchFieldDataType.DateTimeOffset,
                filterable=True, sortable=True),
    SearchField(
        name="content_vector",
        type=SearchFieldDataType.Collection(SearchFieldDataType.Single),
        searchable=True,
        vector_search_dimensions=1536,          # match your embedding model
        vector_search_profile_name="default-vector-profile",
    ),
]

vector_search = VectorSearch(
    algorithms=[HnswAlgorithmConfiguration(name="default-hnsw")],
    profiles=[VectorSearchProfile(
        name="default-vector-profile",
        algorithm_configuration_name="default-hnsw",
    )],
)

index = SearchIndex(name=index_name, fields=fields, vector_search=vector_search)

# --- create it ---
try:
    result = index_client.create_or_update_index(index)
    print(f"create_or_update_index() returned: {result.name}")
except Exception as exc:
    print(f"create_or_update_index() raised: {exc}")

# --- verify independently of the create call's own return value ---
print("\nIndexes now present on this Search service:")
for idx in index_client.list_indexes():
    print(" -", idx.name)
