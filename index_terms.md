## Index terms

### Background

When speaking of "index terms", we may think of a back-of-the-book index in a print work, where there are categories of index terms, and each term points to a page where the term occurs, or where something associated with that term is discussed. To create such a back-of-the-book index, the passages on the pages need to be marked, for example by underlining a term, or by writing a term in the margin. Such a set-up can also work in a digital environment, using hyperlinks, with the difference that page numbers cannot be used; instead the exact location, or range, is given.

This system can also work in TEI, using `<index>` and other elements (see [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CONOIX](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CONOIX)). However, this set-up is designed to digitize existing back-of-the-book indexes, and is therefore less suitable for digitally-born publications like Brill MRWs. Moreover, it does not readily allow unique identification of index terms (esp. according to some external scheme, for example _Library of Congress Subject Headings_) or the insertion of canonical terms, for example the uninflected lemma or regularized version that needs to be included in a back-of-the-book index. For these reasons, Brill uses the `<rs>` element instead, which stands for _referring string_.

### Guidelines

Referring strings are covered in the TEI Guidelines in [Chapter 3.5 Names, Numbers, Dates, Abbreviations, and Addresses](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CONA). As always, TEI  offers a host of options. For reasons of simplicity and uniformity, Brill chooses a minimum number of generic elements based on concrete needs.

### Explanation

The `<rs>` element tags the phrase in the base text that needs to be indexed. Within this tag, `idno@sortKey` can be nested. This sets the sequence of index terms in a list, such as a back-of-the-book index or a browse list. (Not all index terms are necessarily alphabetical, or to be ordered alphabetically). Also, the `<reg>` element can be nested within `<rs>` to document the canonical term. The `@type` attribute indicates the category of index terms, for example "Index Nominum", i.e. index of personal names.

Then the identifiers: `@xml:id` identifies an _element_. This allows, for example, to refer from a browse list of index terms to a phrase in the base text. (This attribute may be used in combination with `<rs>`, `<idno>`, and `<reg>`). The `rs@key` attribute identifies a term according to some external defined scheme. It makes sense to declare such a scheme in a `<taxonomy>` in `<teiHeader>`, and use #values that are equally defined in the `<teiHeader>`. Lastly, `rs@ref` identifies terms with a URI, for example a CITE URN.

### Example
```xml
… A <rs xml:id="brill00001" type="subjects" ref="http://id.loc.gov/authorities/subjects/sh85018111"><idno sortKey="burlesque"/><reg>Burlesque (Literature)</reg>burlesque</rs> is a literary, dramatic or musical work intended to cause laughter …
```

