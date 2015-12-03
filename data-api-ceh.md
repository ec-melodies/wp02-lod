# CEH case study on exposing historic soil moisture data

The following are ideas on how [CEH](http://www.ceh.ac.uk) soil moisture data can be exposed with different APIs,
ranging from generic ones to those which use terms of the application domain within the API URLs.

Each such API is exposed as a DCAT distribution on the "CEH historic soil moisture" dataset.

## Domain model

The application domain is roughly:

- A *site* has multiple *tubes*.
- A *tube* measures soil moisture at specific times and depths (no strictly fixed pattern).
- A *tube* has metadata like location and from when to when it was in use.
- Both a *site* and *tube* have IDs.

## Generic data APIs

A "generic" data API is one which at its core is independent of any application domain concepts.
This includes OGC's W*S, SPARQL, OPeNDAP, or other such endpoints.
See [Coverage Data REST API](https://github.com/Reading-eScience-Centre/coverage-restapi)
for current developments within the University of Reading on creating a versatile and lightweight API.

## Custom API

One of the requirements of CEH is to provide an API which is natural to the application domain.
A natural way for exploring the data using the domain concepts would result in URLs like:
- /sites/
- /sites/1
- /sites/1/tubes
- /sites/1/tubes/A

Those URLs would provide different views via content negotiation, e.g. HTML for web browsers, and
JSON for software libraries.

Since in general each application domain has its own terms and structure, this custom API has to be created from
scratch. It does not match an existing generic data API.
However, this should not be an issue and actually is how the semantic web works, by giving URLs
to things that can then be referenced.

The interesting part is the last level /sites/1/tubes/A. Here, in some way, actual measured data
has to be exposed/referenced.
The granularity of how such data is exposed (each measurement gets its own URL vs. a group of
measurements gets a URL) is to be debated.

To prevent too much work it likely makes sense to reuse generic data APIs at this level.
The resource /sites/1/tubes/A could return a JSON document which contains a data URL to
a generic data API, e.g. a WCS at /sites/1/tubes/A/wcs could contain all the data of
that tube that was ever measured.

By reusing generic data APIs it also becomes easy to reuse tools that can handle such
APIs, like a web tool for visualizing coverages from a WCS/WMS/etc.
See [Coverage Data REST API](https://github.com/Reading-eScience-Centre/coverage-restapi)
for a flexible approach to this.

Depending on the extensibility of the generic data API, one could also think of exposing
*all* data at a single API endpoint and then use custom extension parameters to filter
by domain concepts. For example, /sites/1/tubes/A could contain a link to a generic data API at
/covapi/coverages?siteid=1&tubeid=A. This API could expose various "capabilities", e.g.
general spatial/temporal filtering and subsetting, paging of results, but also a non-standard
capability to filter by site ID and tube ID. The advantage of a single endpoint is that
it can be crawled and handled more easily by generic applications, without the need
to use the domain concept terms and following a URL structure (/sites/1/tubes/A etc.).
This would also allow to directly include such generic data API endpoint as a DCAT distribution,
since it would contain the data of the whole dataset.

## Complexity of having multiple data APIs

Providing multiple entry points to the data of a dataset can become a complex task.
Ideally, there should be a "root" data storage from which all the different
representations are derived by automated transformations (either just-in-time or statically
generated and stored). Every data API is then
strictly a *view* onto the "root" data, which itself could be exposed in some way, but doesn't
have to be (e.g. if the root storage is a DB system).
Manual editing etc should be prevented at all costs.


  