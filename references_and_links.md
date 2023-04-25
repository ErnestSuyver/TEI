## References and links

### Background

"Reference" can mean many things, but in the context of Brill MRWs it is (1) a bibliographic reference to primary sources or to secondary (scholarly) source; (2) a reference from one entry to another (either to the entry as such or to a place within the entry, and either within the same publication or outside it) – which really is a variant of (1); and (3) the relation between a table of contents and an entry, or between an index term and an entry, or between a citation and a bibliographic reference – which is focused on the link between two entities and often conflated with the HTML mechanism of hyperlinks.

Whatever the context, references imply some connection of the type "pointing" between two entities on the basis of an identification. So if the identity of entity A is included in the pointer from entity B to entity A, then there is a reference. Such a reference can take the form of a simple arrow (e.g., "Virgin Birth is discussed in the article on → Mary"), or a "see also" ("For _Horses_, see also _Domestic animals_"), or a bibliographic reference in the Chicago Style, or a hyperlink, or a more complex retrieval system like CapiTainS. Whatever the form, whatever the functionality of the reference, it is built on clear identification.

### Guidelines

See TEI Guidelines [Chapter 3.10 Reference Systems](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CORS) and [Chapter 16.1 Links](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/SA.html#SATS).

### Explanation

Brill references of type (2) and (3) use in XML what TEI calls "linking" rather than "referencing". There are in fact ten linking mechanisms in TEI P5, and Brill mostly uses the one relying on the `@xml:id` attribute. Notice the prefix "xml" in this attribute, which indicates the XML namespace. This means the attribute is prior to TEI; moreover, in TEI it is a global attribute that can be used in anywhere (i.e. in combination with any TEI element). This is because these linking mechanisms are based on the [XPointer framework](https://www.w3.org/TR/xptr-framework/), which is a W3C recommendation. They form an essential part of XML and of the web architecture.

The mechanism works with a pointer-anchor structure. The anchor is any element with an `@xml:id` attribute. Its value must be unique within the XML document. The pointer is also an element, with a special attribute, usually `@target`. The value of this attribute is identical to that of the `@xml:id` attribute. This value turns the pointer into a reference. TEI has several of these pointer type elements, of which `<ref>` is the most versatile and therefore preferred. There are no special anchor elements, with the exception of `<anchor>`, which is used only if no other element is present.  Don't forget to place a hashtag (#) before the target value of using the value of `@xml:id`.

In an attempt to ensure mutual hyperlinks, Brill XML can sometimes contain pointers with identifiers, and anchors with pointers. Also, an anchor may have multiple incoming pointers, and vice versa, leading to multiple anchor identifiers and multiple pointers in or near the anchor (and vice versa).

#### A word about references

In TEI, a link in this sense is not a hyperlink, but a way to lay bare the structure of a text. (In TEI, encoding is textual analysis). The structure in this case is not necessarily linear (as in the stream of a text), or hierarchic (as in the structure of a text). This type of linking can connect disparate elements.

References reveal the structure of a text in a similar way. A references in TEI is not just the mention of a publication, it presupposes a structure. The reference then points to an exact position within that structure. For scholarly literature, this structure is a well-established system of levels: serial – monograph – analytic, for example, or serial – analytic – cite range. It is this reference system that in TEI forms the basis for the Brill references of type (1).

A similar system exists for references to primary sources, i.e. the object of scholarly analysis. There is one difference. References to scholarly publications are often closely connected to particular format, usually print. (Increasingly problematic in the age of digital publications). Not so with references to primary sources. They often follow (for historical reasons) the logical a structure of a work rather than the physical structure of a publication (format). An example is a structure like work – book – chapter, or the previously encountered poem – stanza – line.

The subject of logical structure and its consequences for the XML structure of texts is covered in more detail in the Brill CTS/CITE/CapiTainS Guidelines. Here, it suffices to say that TEI P5 supports this reference system and that Brill uses it for encoding text editions, which are a type of primary sources. TEI, the aim is for the XML to follow the logical structure of a work, for example through nested `<div>` elements. Each of these would have a `@n` (or occasionally `@xml:id`) attribute identifying the structural level or part, thus enabling precise references. Remember that an `@n` attribute simply numbers an element, so this only works if the XML structure follows the logical structure.

#### Referencing in a wider sense

Remember there is also an attribute `@ref`. We encountered in the context of the identification of the author or editor of the document encoded in TEI XML. In the `<titleStmt>` we might encounter something like: `<author><name type="person" ref="http://viaf.org/viaf/93649241">Gizewski, Christian (Berlin)</name></author>`. The attribute here serves to unambiguously identify the entity (an author) referenced here by name (personal name). Like `@key`, `@ref` can only be used to provide _canonical_ information about the referenced entity and hence must have a URI as value. "Canonical" in this context means authoritative, unambiguous, and accessible. So here, too, we have a reference (to an author) but not in one of the three sense above, and the focus here is on the identification rather than the pointer (although a linking system could be built on top of the `@ref` attribute).

#### Example of citation

In another section, we had an example of a citation, i.e. a short form bibliographic item, possibly containing a cite range, referring to its long form elsewhere in the document. 

_It looked like this in the base text:_

```xml
<ref target="a10.1163_2214-8647_bnps5_e326560_bibl_1">[1]</ref>
```

_And like this in the bibliography:_

```xml
<bibl xml:id="a10.1163_2214-8647_bnps5_e326560_bibl_1">
```

#### Example of bibliographical reference

See the section on bibliographies

#### Example of reference to a place in the same entry

See the example of the citation above. Other examples are comments and notes.

#### Example of reference to another entry

Note the use of `@type` to identify the product. This has to be used even if the entry belongs to the same publication as the entry with the references, because at this moment the values of `@xml:id` are only unique with a document.

```xml
<ref type="dnp" target="e119160">Amt</ref>
```

#### Example of reference to a place within another entry
_In the pointer entry, we might have this:_

```xml
<ref type="dnp" target="e119160" n="5">
```

_And in the anchor entry, this:_

```xml
<anchor xml:id="5">
```

If no unique IDs are used, this may also be applied for in-document references.

#### Example of a references to some external resource ("hyperlink")

Note that the surface text of the link (the contents of the `<ref>` element) could simply have been "kluwerlawonline.com" or _Kluwer Law Online_.

```xml
<p>Lim Chong Kin and Ng Ee-Kia, "Singapore," in <hi rendition="#italic">International Encyclopaedia of Laws: Competition</hi> (Kluwer Law International, 2013). <ref target="http://www.kluwerlawonline.com">http://www.kluwerlawonline.com</ref>.</p>
```

### Recommendation

1. For `@xml:id`, use values that are unique within Brill, and not just unique with a document or a publication.

2. At the moment, references to places in Brill MRWs, either within the same publication or outside it, and either on entry level or deeper, look like this in TEI XML: `<ref type="[Product Identifier]" target="[Entry Identifier" n="Anchor Identifier">`. This may be valid xml, but it is not  in keeping with the TEI way. The `@type` and `@n` attributes are abused. The three identifier should be combined into one: the anchor identifier should contain the entry and product identifiers. Hence recommendation (1) above. Use this identifier as the value of `@target` and eliminate the other two attributes.

3. Consider using DOIs to refer to other Brill entries.

