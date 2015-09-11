# Ideas on Web APIs

It seems we converge on using DCAT/GeoDCAT-AP for general dataset metadata, and the distributions of a DCAT dataset to link to the actual data, which can be in form of static files or a service. Let's ignore static files for now.

This means we have two levels on top of which an API could run:
1. DCAT catalogue,
2. actual data.

## DCAT API

Querying DCAT datasets should not be complicated and probably only be very high-level.
It should at a minimum be possible to filter datasets by freeform keywords, spatial and temporal extent. Filtering datasets based on in-depth data knowledge is way more complex to achieve and needs specialised implementations, therefore this should not be the initial focus. 

As far as we know, there are no such APIs in common catalogue software (e.g. CKAN) which then also return DCAT in some form. Looking at CKAN, given the efforts of the ckanext-dcat plugin, it seems that not many pieces are missing.

Given the simplicity of such API, a good method to advertise it in a standard way, once implemented, would be to publish OpenSearch descriptors based on the OpenSearch Geo and Time Extensions (OGC 10-032r8).

Having such an API is crucial for external ingestion (based on LOD principles) and in general machine-readability. However, from a data user point-of-view, it currently doesn't make much difference to have such API, since the user will query with the portal web interface anyway. It is also not very critical for any web portal software using the data, since there *is* a DCAT output for each dataset in CKAN (with a URL that has to be known), and the data can also be directly accessed with the various service endpoint URLs. In summary, it is nice to have and would allow to close the gaps in the linked data world. The API and modelling of the actual data is however likely far more important.

## Data API


