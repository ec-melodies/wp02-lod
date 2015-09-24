# Ideas on Web APIs

It seems we converge on using DCAT/GeoDCAT-AP for general dataset metadata, and the distributions of a DCAT dataset to link to the actual data, which can be in form of static files or services. Let's ignore static files for now.

This means we have two levels on top of which an API could run:

1. DCAT catalogue,
2. actual data.

## DCAT API

Querying DCAT datasets should not be complicated and probably only be very high-level.
It should at a minimum be possible to filter datasets by freeform keywords, spatial and temporal extent, and provide paging. Filtering datasets based on in-depth data knowledge is way more complex to achieve and needs specialised implementations, therefore this should not be the initial focus. 

As far as we know, there are [no](https://github.com/ckan/ckanext-dcat/issues/38) such APIs in common catalogue software (e.g. CKAN) which then also return DCAT in some form. Looking at CKAN, given the efforts of the ckanext-dcat plugin, it seems that not many pieces are missing.

Given the relative simplicity of such API, a good method to advertise it in a standard way, once implemented, would be to publish OpenSearch descriptors based on the OpenSearch Geo and Time Extensions (OGC 10-032r8). That way, simple clients can do keyword-based search, and advanced clients geo/time search.

It should be possible to discover/ingest the full catalogue without knowledge of OpenSearch or URL parameters. This could be done by having a query endpoint that uses paging by default (first request redirects from / to /?p=1&count=100) and providing next/prev navigation via Link HTTP headers. [LDP Paging](https://dvcs.w3.org/hg/ldpwg/raw-file/default/ldp-paging.html) may be a good inspiration for that. By doing that, it should be possible to provide a non-API path to easily access the catalogue e.g. from a crawler or other generic software simply by following the provided next-URLs.

Having such a filter/paging API is crucial for external ingestion (based on LOD principles) and in general machine-readability. However, from a data user point-of-view, it currently doesn't make much difference to have such API, since the user will query with the catalogue web interface anyway. It is also not very critical for any web portal software using the data, since there *is* a DCAT output for each dataset in CKAN (with a URL that has to be known), and the data can also be directly accessed with the various service endpoint URLs if necessary. In summary, it is nice to have and would allow to close the gaps in the linked data world, and also allow for new mesh-portals that integrate multiple catalogues. The API and modelling of the actual data is however likely more important for the time being. Since without data, there is no dataset to be queried.

## Data API

A data API can be anything from a (Geo)SPARQL, Linked Data Fragments, OGC W*S, OPeNDAP, or other endpoint. A dataset can have multiple APIs to represent data in different ways, e.g. WMS for ready-made map layers, and SPARQL for direct data access to do own processing or analysis.

If multiple endpoints exist, then a possible challenge is to create meaningful links between them. For example, a certain WMS layer may cover a subset of the data. Ideally, within the data, this subset is reflected as such in some way and a link to the WMS layer is given. The goal is to make using/exploring the data as easy as possible.

A question that was raised is how to expose data with URLs that follow domain concepts, instead of just having a single SPARQL/WCS/.. endpoint for example. Easy-to-use APIs for the target group are important. The following overview describes how this can be achieved while not letting complexity explode: [CEH case study on exposing historic soil moisture data](data-api-ceh.md).
