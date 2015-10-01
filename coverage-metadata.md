# Metadata for Coverages

The following is related to work discussed in the [CEO-LD project](http://www.w3.org/2015/ceo-ld/) (who provide advice on coverages to the [W3C/OGC Spatial Data on the Web Working Group](http://www.w3.org/2015/spatial)).

## Conceptual View

### A vision of the future

Metadata for coverages can be given on many levels and different forms. A useful way to concentrate on the essentials is to imagine a future global search engine for geospatial datasets similar to simplicity and usability of Google. What would such a search engine crawl? Which details would it need? Which users would use it? What are their needs? How domain-specific does it have to be? How does it crawl datasets? Which formats would it look at? Which would it very likely ignore? How do typical queries from users look like? ...

From this vision, a common denominator must emerge in terms of metadata. Ultimately, one extensible format should exist from which search engines can easily choose to which level they want to go. They could start with indexing basic metadata like title, keywords, producer, spatial region, time range; and over time they could extent to more complex details if they are provided: technical data source (which sensor), data resolution, measured properties (like temperature) etc.

This first vision stops at the metadata level and does not go further. Since actual measurement data can be expressed in many ways and different domains require different formats it is not feasible to select a winner just now. If a search engine still wants to dig into data and provide live previews or other things, then it has to support custom formats. Whichever actual formats for data are used must be clearly identified in the metadata and a link to the data established if possible. Since not all datasets are public this can end at a website for ordering the data. No matter which links are established they should always be unambiguous such that a search engine would know what they mean.

### Legacy data

Sometimes, data is hidden behind web forms and a direct URI to identify a dataset or coverage is not available. In that case it may not be possible to easily provide meaningful metadata for individual dataset elements like coverages. One solution may be to only provide one central metadata for the whole dataset, and in the future see how to improve the data source to support web linkability better.

### What is a coverage? What is a dataset?

To come closer to the vision, we first need to be clear what a coverage and what a dataset is.

The definition of coverages is quite clear, citing [Wikipedia}(https://en.wikipedia.org/wiki/Coverage_data): "A coverage is represented by its "domain" (the universe of extent) and a number of range of values representing the coverage's value at each defined location." This includes metadata of the range values, that is, what the values represent, like wind speed or temperature.

On the other hand, there is no clear definition of what a dataset is. DCAT describes a dataset as a "collection of data, published or curated by a single agent, and available for access or download in one or more formats".

Clearly, a coverage fits the description of a DCAT dataset. But what if a provider groups several coverages as one "dataset" (e.g. many "granules" make up a global dataset)? Is this itself then again a DCAT dataset which consists of those coverage datasets? These are questions to be asked and answered.

From the point of view of a search engine it would make a lot of sense if it could understand such a parent-child relationship. If it didn't understand it and would index both the parent and all its children datasets equally, then it may cause confusion when users search for datasets by geographical region etc. If a search returns a particular coverage described as DCAT dataset, then from an end user point of view it would be very helpful to discover that this coverage is part of a parent dataset, from which the user could explore sibling coverages.

Hence, anything that "contains" data, even if nested within some hierarchy where only the last layer represents the actual coverages, is a dataset. Handling this generic concept is only possible if rich metadata can be expressed on the contents and relationships of such datasets.

### Subsets of Coverages

It is a reoccuring use case to be able to reference subsets of coverages with a unique URI. An example is to annotate a region of a coverage (let's say it is a global grid) with some information, which can even be user feedback.

The CEO-LD group is currently thinking about how those URIs could look like.

More importantly though, in terms of metadata, what would live under such subset URLs if they are dereferencable (which they should be)? Since a subset is again a dataset, it only makes sense to have similar DCAT metadata for that subset, apropriately adjusting the information relevant to the subset (bounding box etc.). And again, to establish the connection to the full "parent" coverage, there must be some link to it.

## Proposed Metadata for Coverages

### Open Issues / TODO

- DCAT doesn't support hierarchies of datasets out-of-the-box. It just knows a Catalog which has Datasets. How can Datasets be related to each other?
- How can a Dataset indicate that it represents a Coverage and not any arbitrary data?
- How can a Dataset indicate that it represents a set of Datasets?
- How can APIs and their type be uniquely identified in Distributions? (use dct:type?)
- What details of coverages should be part of the Dataset metadata? A highly useful candidate is observedProperty(s).
- How can observedProperty(s) be included in DCAT metadata for a Coverage.
- How should multiple Distributions with different file types be advertised if the files live at the same URL exposed via conneg? Browser clients clicking on a link would not set the appropriate Accept header. Should the files etc. always be made available with file extension overriding conneg?

### Metadata
