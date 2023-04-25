## Bibliographies

### Background

Bibliographic references are descriptions of bibliographic items, principally articles and monographs, but also primary sources and media like images, audio and video.

Bibliographic references form the backbone of scholarly publications, and it is of utmost importance that users can navigate this web of references freely and effortlessly. This requires well-structured references and support for mechanisms like reference managers, permanent identifiers  - such as digital object identifiers (DOIs) – and openURL.

### Guidelines

See TEI Guidelines [Chapter 3.11 Bibliographic Citations and References](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#COBI).

### Explanation

We already encountered bibliographic descriptions in the `<teiHeader>`, as information _about_ the publication itself. This section focuses on bibliographic references _within_ the publication, for example in the base text, or in a footnote or in a bibliographical section. In terms of TEI elements, this makes little difference: the `<bibl>` element may be used in all these cases.  The `<bibl>` element is used for loosely structured references – it may even include a `<p>` element or plain text – and is therefore suitable for MRW bibliographies.

There are hundreds of bibliographic formats. TEI XML can be regarded as one of them, but there are differences: XML is not about bibliographic style, XML is about structuring documents, not data, and TEI is about much more than only references. Crosswalks exist between TEI and some of the most common bibliographic formats: [https://wiki.tei-c.org/index.php/Crosswalks](https://wiki.tei-c.org/index.php/Crosswalks).

TEI XLM has the usual bibliographic fields: author, title, publication year, etc. The examples below may serve as explanation. A few special cases need to be singled out:

- Each bibliographic reference gets a unique identifier, using `@xml:id`. Remember that this identifies the tag, not the publication. (The publication is identified by DOI, ISBN, Handle, etc.). This makes it possible, among other things, to refer to the reference.
- The base text may contain bibliographic references in a short form – knows as citations – that correspond to a longer form in a separate bibliographic section, but refer to a particular place within that publication. These are encoded as `<ref>` with a `@target` attribute that has a value that is identical to that of `bibl@xml:id` in the bibliography.
- Sequence information may be set by `idno@sortKey`.
- Brill encodes separate bibliographical sections as follows: `<div type="bibliography">`, followed by `<head>` which could read something like 'Bibliography', followed by `<listBibl>` containing `<bibl>` elements.
- Identifiers for authors, editors, institutions, etc. are actively encouraged (Library of Congress Name Authority File, Virtual International Authority File, International Standard Name Identifier, etc.)
- Identifiers for publications are mandatory: DOI, ISBN,  ISSN. Also URN.
- In case of non-Latin script publications, translations, and  or parallel version, `@xml:lang` may be added
- Similarly a `@type` may be added, if the values of the title levels (see below) offers insufficient information.

Finally a word about representation. There are as many citation styles as there are bibliographical formats: hundreds, if not more. See [https://en.wikipedia.org/wiki/Citation#Styles](https://en.wikipedia.org/wiki/Citation#Styles). Brill uses the Chicago Style (Author-Date version) as its preferred citation style. See [http://www.chicagomanualofstyle.org/tools\_citationguide/citation-guide-2.html](http://www.chicagomanualofstyle.org/tools_citationguide/citation-guide-2.html). The actually styling is not done manually, but by stylesheets – in the MRW CMSs, in the typesetting and print process, and in the online publication process. Remember, this requires well-structured data to work.

#### Example of monograph

A simple example. The editor could have been identified with `@ref="http://id.loc.gov/authorities/names/n88252866.html"` or with `<idno type="lcaf">http://id.loc.gov/authorities/names/n88252866.html</idno>`. Likewise, the data could have been made written as `<date when="1988/>`. Note the "et al." in the `<persName>`.

```xml
<bibl xml:id="a10.1163_1872-9029_EJ_COM_0030_bibl_1">
    <editor>
        <persName>
            <forename>Allan</forename>
            <surname>Brockway</surname>
        et al.</persName>
    </editor>
    <title level="m">The Theology of the Churches and the Jewish People: Statements by the World Council of Churches and Its Member Churches</title>
    <pubPlace>Geneva</pubPlace>
    <publisher>World Council of Churches</publisher>
    <date>1988</date>
    <idno type="ISBN">9782825409329</idno>
</bibl>
```

#### Example of a chapter in a monograph in a series

This is complex structure, ideally requiring a `<biblStruct>`. The different titles are distinguished by the `@level` attribute. TEI P5 supports the following values: "a", "m", "j", "s", and "u". This corresponds to "analytic" (a part of a whole), "monograph", "journal", "series", "unpublished material". This system, following common library practice, constitutes a typology, but `@type` may be added for additional information. Note also the exact notation of the publication date.

```xml
<biblStruct>
    <analytic>
        <author>
            <forename>Albert</forename>
            <surname>Schachter</surname>
        </author>
        <title level="a">Iolaos</title>
    </analytic>
    <monogr>
        <title level="m">Cults of Boiotia</title>
        <imprint>
            <pubPlace>London</pubPlace>
        </imprint>
        <extent>4 vols.</extent>
        <biblScope unit="part">2</biblScope>
    </monogr>
    <series>
        <title level="s">Bulletin of the Institute of Classical Studies Supplements</title>
        <biblScope unit="vol">38</biblScope>
    </series>
</biblStruct>
```

#### Example of article in journal (1)

This article – encoded in the stricter `<biblStruct>` - has a DOI. Note the encoding of the page range.

```xml
<biblStruct>
    <analytic>
        <author>
            <forename>James</forename>
            <forename>H.</forename>
            <surname>Coombs</surname>
        </author>
        <author>
            <forename>Allen</forename>
            <surname>Renear</surname>
        </author>
        <author>
            <forename>Steven</forename>
            <forename>J.</forename>
            <surname>DeRose</surname>
        </author>
    <title level="a">Markup Systems and The Future of Scholarly Text Processing</title>
    <idno type="DOI">10.1145/32206.32209</idno>
    </analytic>
<monogr>
    <title level="j">Communications of the ACM</title>
    <imprint>
        <date>1987</date>
    </imprint>
    <biblScope unit="vol">30</biblScope>
    <biblScope unit="issue">11</biblScope>
    <biblScope unit="pp" from="933" to="947">933–947</biblScope>
</monogr>
<ref type="url">http://xml.coverpages.org/coombs.html</ref>
</biblStruct>
```

#### Example of article in journal (2)

The previous example demonstrated page range. This example, again using `<biblStruct>`, demonstrate a cite range. This is the sort of reference that may occur in a footnote.

```xml
<biblStruct>
    <analytic>
        <author>
            <forname>David</forename>
            <surname>Chesnutt</surname>
        </author>
        <title level="a">Historical Editions in the States</title>
    </analytic>
    <monogr>
        <title level="j">Computers and the Humanities</title>
        <imprint>
            <date when="1991-12">(December, 1991)</date>
        </imprint>
        <biblScope>25.6</biblScope>
        <biblScope unit="pp" from="377" to="380">377–380</biblScope>
    </monogr>
    <citedRange>378</citedRange>
</biblStruct>
```

#### Example of citation in base text

As explained above, a citation is a short reference which is more fully detailed in a separate bibliographic section. Here is an example from _Brill's New Pauly_ (2214-8647\_bnps5\_fulltextxml\_e326560.xml). The base text reads "the little that can be taken or deduced from her work [1]", which cites "Itinerarium Egeriae", ed. A. Franceschini and R. Weber, in: _Itineraria et alia geographica_, vol. 1, 1965, 27–92. This is encoded thus:

_base text_
```xml
<p> … the little that can be taken or deduced from her work <ref target="1">[1]</ref> … </p>
```

_bibliography_
```xml
<bibl n="1" xml:id="a10.1163\_2214-8647\_bnps5\_e326560\_bibl\_1">
    <author>
        <forename></forename>
        <surname></surname>
    </author>
    <title level="a">Itinerarium Egeriae</title>
    <editor>
        <forename>A.</forename>
        <surname>Franceschini</surname>
    </editor>
    <editor>
        <forename>R.</forename>
        <surname>Weber</surname>
    </editor>
    <title level="m">Itineraria et alia geographica</title>
    <date>1965</date>
    <biblScope unit="volume">1</biblScope>
    <biblScope unit="page">27-92</biblScope>
</bibl>
```

Note that `@target` cannot take "[1]" as value, only "1". A more elegant solution would be to use the `bibl@xml:id` as value for `ref@target`.

### Recommendation

1. TEI recommends the use `<biblStruct>` instead of `<bibl>` in the context of automatic data processing. While the `<bibl>` is used in loosely structured references, `<biblStruct>` allows for stricter ones. Given that working with bibliographical data is a recent development in MRWs, it makes sense to start with the use of `<bibl>` and evaluate the need for `<biblStruct>` after a year or so.

2. Authors and Brill staff tend to spend much attention to the styling of references. This energy is better directed to data quality: good data leads to good styling. In fact, this approach saves energy, as many authors already use reference managers. Brill should investigate ways of processing this data and incorporating them in the present workflows.

### Appendix

Brill MRWs rely on authors and Brill staff to provided (structured) bibliographical data, usually in the route form MS Word to the MRW CMSs. Brill also uses two tools for the automatic conversion of unstructured references into structured ones:

1. the _bibliographical entity recognition_ tool (BER) which recognizes bibliographical data on the bases of typographical features;

2. _AnyStyle_, a self-learning algorithm. Neither can substitute human effort, but they go a long way in the conversion. In 2017, all then MRW entries were transformed into TEI XML and all bibliographic references structured.

