# Metadata for Coverages

The following is related to work discussed in the [CEO-LD project](http://www.w3.org/2015/ceo-ld/) (who provide advice on coverages to the [W3C/OGC Spatial Data on the Web Working Group](http://www.w3.org/2015/spatial)).

## A vision

Metadata for coverages can be given on many levels and different forms. A useful way to concentrate on the essentials is to imagine a future global search engine for geospatial datasets similar to simplicity and usability of Google. What would such a search engine crawl? Which details would it need? Which users would use it? What are their needs? How domain-specific does it have to be? How does it crawl datasets? Which formats would it look at? Which would it very likely ignore? How do typical queries from users look like? ...

From this vision, a common denominator must emerge in terms of metadata. Ultimately, one extensible format should exist from which search engines can easily choose to which level they want to go. They could start with indexing basic metadata like title, keywords, producer, spatial region, time range; and over time they could extent to more complex details if they are provided: technical data source (which sensor), data resolution, measured properties (like temperature) etc.

This first vision stops at the metadata level and does not go further. Since actual measurement data can be expressed in many ways and different domains require different formats it is not feasible to select a winner just now. If a search engine still wants to dig into data and provide live previews or other things, then it has to support custom formats, which must be clearly identified and linked from the metadata.

