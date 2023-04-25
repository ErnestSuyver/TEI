# TEI header

## Background

Each Brill publication carries with it a considerable amount of information about the work itself, its source, its revisions, and (if applicable) its encodings and schemas. The purpose of this information –  sometimes called metadata – is to make the work accessible and discoverable for scholars who use it, applications that process it, and librarians that catalogue it. To achieve this purpose, such information is declared in a formal way. In TEI, this is done in the TEI header.

## Guidelines

See TEI Guidelines [Chapter 2 The TEI Header](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html).

## Explanation

Each TEI conformant XML file consists of a metadata section, called TEI header, and a section for one or more texts, the `<body>`. The TEI header describes the encoded work and so documents the text itself, its source, its encoding, and its revisions.

The TEI header is tagged as `<teiHeader>` and has five major parts:

- a file description, containing a full bibliographical description of the _file_. The XML file can be regarded as the primary manifestation of a work (usually a text) when it is created directly and firstly in XML. This is the case for most Brill MRWs. However, some Brill MRWs are digitations of existing works, e.g. primary source publications or conversion projects,. In such case, the file description describes the digitization effort, not the original work.
- an encoding description, containing information how the source (if any) was encoded or analyzed. Brill uses this to provide information about the file structure, the required CSS version (to render the HTML generated from the XML), and multiple font renderings.
- a description of the text profile containing classificatory and contextual information about the text, used mainly by Brill to provide abstracts, language information, and keywords.
- a container element allowing the inclusion of metadata from non-TEI schemes such as MARC (MARCXML or MODS) or Dublin Core.
- a revision history used for version control.

The following subsections discuss each of these parts.

## '<fileDesc>'

### Background

Brill needs to record bibliographical data concerning its publications. The TEI element `<fileDesc>` in the `<teiHeader>` is the place to do so. This element is mandatory.

The name of the element `<fileDesc>` suggests a "file description", but is a description of the work _manifested in the file_ rather than of the file itself. This is because the file, an XML file, can occur in multiple places in the production and publication workflow; and it is the work that interests its users, not the file. Note that `<fileDesc>` does not describe previous or other manifestations of the work. Within the `<fileDesc>` element, TEI has three large components: `<titleStmt>`, `<publicationStmt>`, and `<sourceDesc>`. Their use by Brill is explained below, starting with the title statement.

### Guidelines

See TEI Guidelines [Chapter 2.2 The File Description](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD2). As always, TEI  offers a host of options. For reasons of simplicity and uniformity, Brill chooses a minimum number of generic elements based on concrete needs.

#### Explanation – Title Statement
Brill uses `<titleStmt>` to store information about (1) the title of the publication in `<title>`; (2) the author or editor in `<author>` or `<editor>`; (3) the funder in `<funder>`. "Publication"  in this context is usually an entry in a reference work. For the author, first name and last name are recorded in `<forename>` and `<surname>`, as well as some identifier, such as ORCID, VIAF or ISNI in `@ref`. Funder is currently not used – hence the value "placeholder" is currently used as default – but is expected to gain importance as Open Access becomes more wide-spread. No doubt funder name and identifier will be recorded, particularly the FundRef ID.

A `@level` attribute to `<title>` indicates that the publication is a part of a greater whole: an entry in a reference work. TEI uses the value "a" (for "analytic") in these cases. This value, and the encoding of bibliographic data in general, is covered in more detailed in the section on bibliographies.

A further attribute, `@sortKey`, indicates the sort order of the title if it contains non-alpha-numerical information or if a special sequence is required. This information is not attached to `<title>` but to an additional (and otherwise empty) element, `<idno>`, which also carries a `@type="sort"` attribute.

The title statement may further contain a `<respStmt>` element, stating who else was involved in the publication, e.g. the person responsible for the translation or the digitization.

#### Example – Title Statement

```xml
<titleStmt>
    <title level="a">Philological and Historical Commentary on Ammianus Marcellinus XXII</title>
    <title level="s">Ammianus Marcellinus Online</title>
    <author ref="http://viaf.org/viaf/32019540">
        <name type="person">
            <forename>J.</forename>
            <surname>den Boeft</surname>
        </name>
        <idno type="ORCID">https://orcid.org/0000-0001-6606-2405</idno>
        <idno type="ISNI"/>
    </author>
    <funder ref="placeholder"/>
</titleStmt>
```

#### Explanation – Publication Statement
In the publication statement, Brill records the following: (1) publisher – usually Brill, but could also be an imprint; (2) publication date; (3) date; (4) digital object identifier (DOI) of the publication (i.e. entry); (5) product identifiers for access management systems – either the "sams-id", or "publisher-id", or both; (6) information about the conditions of use, particularly the availability, with the status values of "free", "restricted" or "unknown" and the Creative Commons license.

#### Example – Publication Statement

```xml
<publicationStmt>
    <publisher>BRILL</publisher>
    <pubPlace>Leiden | Boston | Singapore</pubPlace>
    <date>2018</date>
    <idno type="DOI"/>
    <idno type="sams-id"/>
    <idno type="publisher-id">AMO<idno/>
    <idno type="ISSN"/>
    <availability status="restricted">
        <licence target="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)</licence>
    </availability>
</publicationStmt>
```

#### Explanation – Source description
The source description describes the work of which the entry forms a part. It gives (1) the title; (2) the author or editors (again with first  name, last name, and identifier); (3) publisher; (4) place of publication; (5) publication date; (6) work identifier like ISBN or ISSN. This information is placed in a `<bibl>` element in a `<sourceDesc>` element. More about `<bibl>` and bibliographic data can be found below.

#### Example – Source description
```xml
<sourceDesc>
    <bibl>
        <title level="m">Philological and Historical Commentary on Ammianus Marcellinus XXII</title>
        <author ref="http://viaf.org/viaf/32019540">
            <name type="person">
                <forename>J.</forename>
                <surname>den Boeft</surname>
            </name>
            <idno type="ORCID"/>
            <idno type="ISNI"/>
        </author>
        <publisher> Egbert Forsten</publisher>
        <pubPlace>Groningen </pubPlace>
        <date>1995</date>
        <idno type="ISBN">90 6980 086 1</idno>
    </bibl>
</sourceDesc>
```

### Recommendation

1. Always name the translator (and put them in `<respStmt>`).
2. Add the authors' affiliation, using `<affiliation>` and `<orgName>` in `<author>` or `<editor>`.
3. Currently, `<revisionDesc>` (see also below) is used to record previous publication dates. (Remember, an XML file can serve as the basis for both print and online publications). Such information might be more clearly stored in the source description.
4. There is potential overlap between `<titleStmt>` and `<sourceDesc>`. For now, Brill has placed entry ("part") information in the former – with the exception of the entry identifier, which is an attribute of the root element – and reference work ("whole") information in the latter. Consider a more intuitive arrangement.

## '<encodingDesc>'

### Background

Brill wishes to record the required CSS stylesheets to render the XML files in an HTML environment, as well as various items related to font and type. The TEI element `<encodingDesc>` in the teiHeader is the place to do so. It is also the place for two more specialize features.

### Guidelines

See the TEI Guidelines [Chapter 2.3 The Encoding Description](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD5).

### Explanation

The `<encodingDesc>` element is the second major subdivision of the TEI header. In Brill XML, it is mandatory. In TEI, this element specifies the methods and editorial principles used when encoding ("XML-izing") the document. (Elements with names like `<projectDesc>` or `<editorialDecl>` give a flavor of its intended use). In Brill XML, however, it is used to convey information about rendering and functionality to subsequent parsers. There are four points of information.

- Stylesheet information. Within `<encodingDesc>`, a `<styleDefDecl>` element declares the requires version of the Cascading Style Sheets: `<styleDefDecl scheme="css" schemeVersion="3.0"/>`
- Font and type information. Presently, Brill allows the italic, bold, underline, subscript, superscript, and smallcaps types for its fonts. Such information is found in a `<tagsDecl>` element wrapped in `<encodingDesc>`, for example as follows: `<tagsDecl><rendition xml:id="italic">font: italic;</rendition></tagsDecl>`. Any element that carries the `@rendition` attribute with the value "#italic" will have its contents rendered in the italic type by the stylesheet.
- Information about subjects and keywords. Within `<encodingDesc>`, a `<classDecl>` element may declare classification schemes. Brill doesn't use this at the moment. (Instead, a classification like the Brill-internal subjects are listed in `<textClass>` in `<profileDesc>`). But it makes sense to do so, in terms of discoverability, transparency and interoperability, and so it is good to know it is possible. The actual tagging may look something like this: `<taxonomy><category><catDesc><term>`
- Citation information. This is particularly relevant for text editions and hence explained in the Brill CTS/CITE/CapiTainS guidelines. It boils down to this: in `<encodingDesc>`, there is a `<refsDescl>` element containing a `<cRefPattern>` which defines X-paths. This mechanism allows applications to take a reference and locate the relevant text part in the document. It acts as a bridge between a reference (with a formal syntax, as defined by CITE) and an XML file (likewise CITE-compliant).

### Example
```xml
<encodingDesc>
    <styleDefDecl scheme="css" schemeVersion="3.0"/>
    <tagsDecl>
        <rendition xml:id="italic">font:italic;</rendition>
        <rendition xml:id="bold">font:bold;</rendition>
        <rendition xml:id="underline">font:underline;</rendition>
        <rendition xml:id="subscript">font:subscript;</rendition>
        <rendition xml:id="superscript">font:superscript;</rendition>
        <rendition xml:id="smallcaps">font:smallcaps;</rendition>
    </tagsDecl>
</encodingDesc>
```

### Recommendation

For purposes of discoverability, it is highly recommended to replace the idiosyncratic Brill subjects by subjects that follow an internationally accepted standard, such as the Library of Congress Subject Headings (LCSH). Declare the subjects in a `<textClass>` element.

A crosswalk from the idiosyncratic Brill subjects (used in MRWs) to LCSH subjects is found below. Note that no simple 1:1 crosswalk is possible, because LCSH constitutes a complex system of thought, with its own structure and choices.

### Subjects Crosswalk

| **Idiosyncratic Brill subject** | **LCSH subject** | **URI** |
|-------|--------|--------|
| African Studies | Africa | http://id.loc.gov/authorities/subjects/sh85001531 |
| Biblical Studies | Bible--Study and teaching | http://id.loc.gov/authorities/subjects/sh85013718 |
| Classical Studies | Classical languages | http://id.loc.gov/authorities/subjects/sh85026704 |
| History | History | http://id.loc.gov/authorities/subjects/sh85061212 |
| International Relations | International Relations | http://id.loc.gov/authorities/subjects/sh85067435 |
| Jewish Studies | Jews--Study and teaching | http://id.loc.gov/authorities/subjects/sh85070451 |
| Language and Linguistics | Linguistics | http://id.loc.gov/authorities/subjects/sh85077222 |
| Law | Law | http://id.loc.gov/authorities/subjects/sh85075119 |
| Middle East and Islamic Studies | Islam | http://id.loc.gov/authorities/subjects/sh85068390 |
| Religious Studies | Religion | http://id.loc.gov/authorities/subjects/sh85112549 |

## '<profileDesc>'

### Background

It is often useful to provide more information about a publication than mere bibliographical details. In particular, Brill wishes to record (1) abstract; (2) languages; and (3) keywords. In TEI XM, the optional `<profileDesc>` element is the place to do so.

### Guidelines

The TEI Guidelines describe this element in [Chapter 2.4 The Profile Description](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD4). As always, TEI offers many options – for example, the element may be used to describe the situation in which the document was produced, the participants, and their setting – but these Guidelines confine themselves to Brill's present needs.

#### Explanation - abstract

Nested in `<profileDesc>`, one or more `<abstract>` elements house the abstracts. Use the universal `@xml:lang` attribute to state the abstract's language. Use `<p>` elements to store text blocks.

#### Example – abstract
```xml
<abstract xml:lang="eng-lat">
	<p>Originally founded to aid and defend pilgrims in the Holy Land, the crusading orders soon expanded their activities to the military defense of Christendom from its internal and external enemies.</p>
</abstract>
```

#### Explanation – languages

The `<language>` element declares which languages are used in the document. (Distinguish this from the `@xml:lang` attribute in the `<teiHeader>` which declares the language of the document's metadata). Nested within it sits the `<language>` element. This is a closed elements that declares the language through a value of its `@ident` attribute. This attributes identifies the language in a formal way: it is uses the international standard of BCP 47 codes: [https://tools.ietf.org/html/bcp47](https://tools.ietf.org/html/bcp47).

If the language is indicated for particular parts of the document with the use of `@xml:lang` – in Brill publications, this is often the case – then the exact values of `@ident` must be used.  More information about Brill's use of these tags and BCP 47 can be found in a separate section of these guidelines.

#### Example - languages
```xml
<langUsage>
    <language ident="en"/>
</langUsage>
```

#### Explanation - keywords

Brill uses two different kinds of keywords:

1. Brill subject classification of publication and hence the documents within it, e.g. "History" or "Classics"

2. Keywords classifying a document, usually assigned in the MRW CMSs. In a special case, such keywords are used to create search facets on the Brill publication platform.

 Within the `<textClass>` element, the `<keywords>` element houses the keywords. Within it, each keyword is placed with in a `<term>` element. Brill uses the `keywords@ana` attribute to state the class of keywords; these are the search facets on the platform. The `keywords@scheme` attribute identifies the scheme. For now, the default value is "brill:subject".

#### Example of type 1 keywords
```xml
<textClass scheme="brill:subject">
    <keywords><term>History</term></keywords>
</textClass>
```

#### Example of type 2 keywords (with `@ana`)
```xml
<textClass>
    <keywords ana="#classification\_region">
        <term>Asia</term>
    </keywords>
    <keywords ana="#classification\_country">
        <term>China, People's Republic of</term>
    </keywords>
</textClass>
```

### Recommendation

1. For reasons of discoverability and interoperability, it is strongly recommended to use a recognized international subject classification instead of the proprietary scheme in current use. See the **Appendix on Subject terms** for a proposal using the Library of Congress Subject Headings.

2. The present solution of storing keyword categories in `keyword@ana` is simple, but not completely in line with TEI. It would be better to define the scheme in a `<taxonomy>` element in `<classDecl>` (itself in `<encodingDesc>` and then refer to it in a `<catRef>` element in `<textClass>`.

## \<xenoData\>
The optional element [**xenoData**](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-xenoData.html) (outside metadata) provides a container element into which metadata in non-TEI formats may be placed. Think of MARC21 or Dublin Core records, or RDF triples.

See [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD9](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD9)

## '<revisionDesc>'

### Background

How to manage changes to documents, either before or after publication? TEI XML allows for a "change log" in the `<teiHeader>` element. This may be used in combination with a version management system, for example as part of a content management system.

### Guidelines
The change log is covered in the TEI Guidelines, chapter 2.6 The Revision Description: [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD6](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/HD.html#HD6)

### Explanation

The change log takes the form of a `<revisionDesc>` element. Nested in it are `<change>` elements, which may take the following attributes: `@when` to document the precise revision date, `@type` to document the sort of revision, e.g. "correction", and `@who` to document the person making the change. A `@status` attribute can be used to document the status of the revision or the revised document, e.g. "draft". It is also possible to group `<change>` elements in a `<listChange>` element. The contents of the `<change>` element can be used to describe the change.

TEI strongly recommends the use of this element: "No significant change should be made in any TEI-conformant file without corresponding entries being made in the change log". Brill follows this advice, focusing on changes _after publication_. 

At present, Brill distinguished three statuses of a document after publication:

1. first-online. A document has this status when it is published in print _first_ and online _later_. The print date is then found in the `<publicationStmt>`.

2. first-print. A document has this status when it is published online _first_ and in print _later._ The online publication date is declared in `<publicationStmt>`.

3. last-update. A document has this status when it is revised after publication, usually online.

These three status are added as values of the `@status` attribute to the `<revisionDesc>` element.

### Example
```xml
<revisionDesc status="last-update" when="20170623" status="correction" who="Angelos Chaniotis"/>
```

### Recommendation

1. In the current scheme, statuses like "first-update", "second-update", etc. are missing. Use them instead of "last-update" which is to be avoided.
Also, generate such information from a version management system, not manually.

2. Only use `<sourceDesc>` (see also above) for the source in a conversion project.

3. Use `<publicationStmt>` (see also above) in the following manner:

```xml
<publicationStmt>
    <publisher>Brill</publisher>
    <pubPlace>Leiden | Boston</pubPlace>
    <date>2018</date>
    <idno></idno>
    <idno type="DOI"/>
    <idno type="publisher-id">AMO</idno>
    <idno type="ISSB"/>
    <availability status="restricted">
        <licence target="placeholder">Placeholder</licence>
    </availability>
</publicationStmt>
```
These `<idno>` elements are now found in `<bibl>` in `<sourceDesc>`. Also, place `<title level ="a">` (and `<title level ="m">` or `<title level ="s">` in `<titleStmt>`, followed by first the author of the entry and then the editor of the MRW as whole.

4. Add `@type` and `@when` attributes to the publication date, e.g. `<date type="online" when="20061001">2006</date>`.
