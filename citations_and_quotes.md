## Citations and quotes

### Background

Citations and quotes are two variants of text reuse. TEI considers a quote (or quotation) to be any sort of rephrasing, either oral or written, with or without attribution. It uses citation in a stricter sense: a quotation from another text that is identified though a bibliographical reference.

### Guidelines

In the TEI Guidelines [Chapter 4.3 Grouped and Floating Texts](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DS.html#DSGRPF), the basics can be found. More about quotation is found in [Chapter 3.3.3 Quotation](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#COHQQ).

### Explanation

A quotation may occur on its own in a text, so one might have a `<quote>` somewhere in a `<p>`. If it is a citation, the `<quote>` element is wrapped in a `<cit>`, and a `<bibl>` element is added. (More information on `<bibl>` is found in the section on bibliographies). All sorts of refinements are possible, e.g. the use of `@type` with "original" and "translation" for `<quote>`, or the use of `@xml:id` for purposes of reference.

The above applies to secondary literature. If a primary source is quoted, the `<quote>` element sits within a `<ref>` element, to which a `@target` attribute with a CTS URN may be added. The reverse order is also possible: a `<cit>` wrapping both `<ref>` and `<quote`.

#### Example 1 – citation of primary source

```xml
<ref target="urn:cts:brill.bra00010.brw00001.296.11">
    <cit type="example">
    <quote xml:lang="grc-Grek">ἐπεὶ οὖν τῷ ἀληϑῶς ἀγαϑῷ πρὸς τὸ μή άληϑῶς ἀγαϑόν έστιν ἡ ἀ., ἀμεσος δὲ τῶν δύο τούτων ἡ έναντίωσις</quote>
    <bibl>34,34,9</bibl>
    </cit>
</ref>
```

#### Example 2 – citation of primary source

```xml
<cit>
 <ref cRef="Jon 1:17"/>
 <quote> And Jonah was in the belly of the fish three days and three nights.</quote>
</cit>
```

#### Example – citation of secondary literature

```xml
<cit>
    <quote xml:lang="pt-Latn">Os fundadores das sociedades de seguros mútuos não eram, necessariamente, trabalhadores altamente qualificados.</quote>
    <bibl>M. van der Linde, Trabalhadores do mundo, p. 128</bibl>
</cit>
```

### Recommendation

Although there is considerable scholarly interest in text reuse, quotations can be hard to identify. Fortunately for Brill, the authors and editors have done the hard work for us. Quotation marks, italics, and other typographical features are used to mark quotes. Should these marks be retained in the XML documents, or relegated to the stylesheet as a matter of representation? The answer may depend on the text (a quotation mark in a primary source may need to be preserved) but in any case the recommendation is to make an agreement about this with the typesetters and platform people. This will allow Brill to make the right choice for the XML. It is good to know that TEI has several options (e.g. `@rendition="#dashBefore"`, or `@rend="pre(') post(')"` or defining a CSS scheme for a given element in the `<tagsDecl>`). Hard-coding is not recommended.

