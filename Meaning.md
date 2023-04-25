# Meaning
XML – and therefore TEI – is concerned with the _structure_ of a text, for example the difference between a header and a text block, or between an author and a work. Of course, these differences _mean_ something; `<head>` and `<author>` are meaningful tags. Also, there is an attribute like `@type` that can be used to indicate the meaning, not of the structure, but of the very content itself. To this extent, TEI can be said to be _semantic_ as well as syntactical. However, these tags have no meaning outside the world of TEI, and they are not machine readable. (A parser can react on the present of `<head>` without identifying a header as such; any such reaction would always be application-specific; there is no way of knowing that `<head>` in a non-TEI document has the same meaning). Therefore, TEI _cannot_ be said to be semantic in the sense of having uniform, machine-readable, meaningful tags, based on ontology that defines classes and properties.

How then can Brill ensure optimal discoverability of its content? How then can Brill ensure interoperability with other, possibly non-TEI compliant resources? After all, users are interested in people, places, and subjects, not in structure or application-specific niceties. One way is shown in these guidelines: the use of `@type`, with the values declared in the metadata.

This way can be strengthened by using additional semantic, or semi-semantic tags. The list below gives some of the most widely used categories of information in Brill MRWs. Some MRWs already have some such tags and it makes sense to take a more uniform approach.

## Meaningful tags in TEI P5

| Categories | TEI P5 element | TEI P5 Explanation | Annotation |
| ---- | ---- | ----- | ---- |
| **people** | `<persName>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-persName.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-persName.html) |   |
| **organizations** | `<orgName>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-orgName.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-orgName.html) |   |
| **places** | `<placeName>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-placeName.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-placeName.html) |   |
| **periods** | `<date>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-date.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-date.html) |   |
| **subjects** | `<rs>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-rs.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-rs.html) | A subject or keyword that describes the entry contents as such is **metadata** and is encoded `<term>` in `<textClass><keywords>` |
| **authors** | `<bibl><author>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-author.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-author.html) |   |
| **works** | `<title>` | [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-title.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-title.html) |   |

However, this solution is still application-specific. There is an alternative, or rather, additional, approach: the adoption some of the practices of _Linked Data_. This is a way to unambiguously establish the meaning of data, and to string together such data into meaningful wholes. It builds on standard Web technologies such as HTTP, RDF, and URIs. Resources adopting Linked Data standards can connect, share and exchange data. Linked Data is primarily aimed at machine consumption, although the same information can of course also be offered in human readable form.

Tim Berners-Lee, director of the World Wide Web Consortium (W3C), coined the term "Linked Data" in 2006 and outlined these four principles:

1. Use [URIs](https://en.wikipedia.org/wiki/Uniform_resource_identifier) to name (identify) things.
2. Use [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) URIs so that these things can be looked up (interpreted, "dereferenced").
3. Provide useful information about what a name identifies when it's looked up, using open standards such as [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework), [SPARQL](https://en.wikipedia.org/wiki/SPARQL), etc.
4. Refer to other things using their HTTP URI-based names when publishing data on the Web.

It is not necessary to take all these steps at once. It is already immensely helpful to take the first step – which may easily combined with the second. A key role here is played by identifiers – not so much identifiers of elements, but of the encoded entities. We already encountered identifiers of authors and editors in the form of the VIAF URIs that act as values for the `@ref` attribute in `<name>`. This approach can be applied more uniformly, and combined with the use of the (semi)semantic tags listed above.

The next step would be to connect these (semi)semantic tags to authoritative and widely used ontologies such as CIDOC-CRM and FRBRoo. This is about the identification of the classes rather than the instances. See [these](http://www.edd.uio.no/artiklar/tekstkoding/poster_156_eide.html) pertinent remarks. This will significantly boost the discoverability of the content of Brill MRWs. There are numerous other advantages, in terms of content enrichment and improved search and browse options. Most importantly, perhaps, it will root Brill publications deeper in the communities of scholars using these resources.

The (semi)semantic tags listed above overlap with indexes (or index categories) found in Brill publications, for example as back-of-the-book indexes in print MRWs. (There are many indexes that are not included in this list, but the vast majority of indexes are of the type "people/names", "subjects/things", and "places"). At this moment, many Brill MRWs that are published online have on their homepages browse lists composed of index terms that link to entries in which these terms occur. This is the digital equivalent of the back-of-the-book index in print volumes.

Familiar and useful as they are, such browse lists are not the only functionality that can be built on top of index terms. When turned into linked data, they can be used to associate other information from other resources with, and made to drive search and browse tool, including timelines, maps, slideshows, networks, and other data visualizations. In this way they open up Brill content in new and useful ways and so fulfill their role as discovery tools optimally.

The first step is already taken – the allocation of unique identifiers for instances and (semi)semantic tags for classes. The guidelines for the syntax of such identifiers can be found in _RFC 3986 Uniform Resource Identifier (URI): Generic Syntax_, a [document](https://www.ietf.org/rfc/rfc3986.txt) by the _Network Working Group_ of the _Internet Engineering Task Force_. Given the goal of standardization, it makes sense to use existing URIs. For example, the Brill CTS/CITE/CapiTainS Guidelines give the syntax of identifiers for canonical texts.
