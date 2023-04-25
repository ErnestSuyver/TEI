# Presentation
Presentation, like functionality, is covered in depth in a separate document: `G:\Projects\TripleC\enc2teip5\0.1 Manual\MRWs on CCC\MRWs on CCC.docx`. Therefore, the following remarks suffice here.

As stated above on several occasions, Brill MRW staff needs to be able to influence the presentation of MRW publications. There are several ways to do this, going from generic to specific:

- Creation of an MRW Style guide. Its rules apply to both print and online
- Creation of procedures to create, change, or delete stylesheets used by the typesetters. This is a direct relation between MRW staff and a supplier
- Creation of procedures to create, change, or delete stylesheet used by platforms. This is an indirect relation, involving MRW staff, PT staff, and possible Brill project teams. No direct contact with the supplier is possible.
- Creation of generic XML mechanisms to influence stylesheets
- Creation of options to actually implement these XML mechanism, for example through functionality in the CMSs
- Creation of options to implement an individual feature of presentation.

This manual is largely concerned with the creation of generic XML mechanisms to influence stylesheets. We encountered three major ways to accomplish this:

1. Font representations: italics, small caps, etc. Use of `@rendition` in combination with `<rendition>` in `<tagsDecl>`.
2. Representation of (characters in the correct) fonts. Use of `@xml:lang` in combination with `<languages>` in `<langUsage>`.
3. Representation of properties of e.g. tables and writing systems. Use of `@style` in combination with CSS values (value pairs, value triples).

Note that there is a problem with `@rendition`: the TEI Epidoc customization only allows `@rend`. So if a document validates against both the generic TEI schema (tei\_all.rng) and the Epidoc schema (tei-epidoc.rng) it is not possible to use `@rendition`; instead, use `@rend`.
