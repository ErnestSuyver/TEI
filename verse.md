## Verse

### Background

Brill content may contain poetry and other non-prose text types. Think of text editions, quotes, or examples in linguistic publications. There is no `<poem>` tag in TEI, because that would be semantic, whereas XML is syntactic. But there are ways to deal with text typology and the structure of non-prose text types. Likewise, there are no tags that determine the appearance of say, a poem, but a stylesheet can be made to work on the structural tags.

### Guidelines
The basics of verse and related subjects are covered in the TEI Guidelines [Chapter 3.12 Passages of Verse or Drama](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CODV). As always, TEI offers many more options. Segmentation, rhyme, and metrical analysis, for example, are covered in [Chapter 6 Verse](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/VE.html). For reasons of simplicity and uniformity, Brill chooses a minimum number of tags based on concrete needs.

### Explanation

Text type can be indicated as values of `@type` attribute. TEI regards the line as the fundamental unit of text of the type "verse", and for this Brill uses the `<l>` element. Lines can be grouped in an `<lg>` element which may be further grouped. For example, a `<lg type="sonnet">` may contain a `<lg type="octet">` and `<lg type="sestet">`.

Note that an `<l>` does not denote a typographic line, but rather a metrical unit. A typographical line is indicated by `<lb/>`, which stands for "line beginning" (and not "line break "). For verse, use `<l>`. For other text types, use `<lb/>`.

### Example
```xml
<lg n="Chorus" type="refrain">
    <l>Then a Mohock, a Mohock I'll be,</l>
    <l>No Laws shall restrain</l>
    <l>Our Libertine Reign,</l>
    <l>We'll riot, drink on, and be free.</l>
</lg>
```

### Recommendation

If text types are used, declare a scheme in the teiHeader that defines the values (e.g. "verse", "prose", etc.).

