# Validation

There are two basic checks if XML is "correct": well-formedness and validity. Well-formedness is a property of XML as such: do the tags have angle brackets? Is the opening tag followed by a closing tag? And so on. Validity is a property of a given XML language: does the document use the tags in that language? Do these tags occur in the allowed combinations? The rules for this language need to be laid down somewhere. This is not the purpose of the guidelines of the TEI Consortium. These describe what _can_ occur. But it is a purpose of these Brill TEI Guidelines. These also describe what can occur, but sometimes also what _must_ (or _must not_) occur.

Of course, these guidelines are written for human consumption. However, processing large amounts of XML at high accuracy rates requires automatic validation. Any XML parser can do this – Brill uses Oxygen, which is a powerful tool with full support for TEI and an excellent customer service. But the parser needs a machine-readable document. This is called a "schema" and the following section explains how to create and use it.

## Schema

First off: a schema contains constraints on the structure and content of XML files. A schema is itself expressed in XML. There are in fact several languages to create a schema, such as the [Document Type Definition](https://en.wikipedia.org/wiki/Document_Type_Definition) (DTD) language, [XML Schema](https://en.wikipedia.org/wiki/XML_Schema_(W3C)) (with a capital _S_), and [RELAX NG](https://en.wikipedia.org/wiki/RELAX_NG). (The latter is a short form of XML, called "compact syntax"). Being XML, a schema is both human and machine readable. There is a simple mechanism for associating an XML document with a schema: markup within the XML document itself. This happens even before the teiHeader. It is a pointer in the root element. We encountered this above in the following form: `TEI@xmlns:rng="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng"`.

Brill prefers RELAX NG (REgular LAnguage for XML Next Generation) because it is adopted as primary schema by TEI and because it is an ISO standard. (ISO/IEC 19757-2 was developed by [ISO/IEC JTC1/SC34](https://en.wikipedia.org/wiki/ISO/IEC_JTC1/SC34) and published in its first version in 2003). It supports data typing, regular expression, namespaces, and the ability to reference complex definitions. See [http://relaxng.org/](http://relaxng.org/).

At this moment, Brill XML that is TEI P5 compliant is associated with the widest, most permissible, all-encompassing schema, tei\_all.rng. It remains to be seen whether this is always the most helpful choice. It may well be that scholarly editors working on a publication in a dedicated CMS, or suppliers working on the conversion of a complex MRW, requires a more narrow, more focused schema.

TEI offers a tool to create one's own schemas. It is called _Roma_ and can be found here: [http://www.tei-c.org/Roma/startroma.php?mode=main](http://www.tei-c.org/Roma/startroma.php?mode=main). It allows you to select elements and attributes you need, and deselect the one you don't. This results in a so-called ODD file. This stands for "One Document Does it all". An ODD file is itself a TEI XML file. From the ODD file, a schema can be created. Roma supports the three major schema languages. An ODD file is only just human readable (it's very formal) but it is TEI so human readable information can be added. (Although that hasn't been done by Brill so far; these guidelines stand beside the ODD file and the Relax NG file; none of them replaces the others).

## Schematron

Roma allows for some constraints on attribute values. For more refined settings, we must turn to schema languages such as RELAX NG directly. Examples are Boolean predicates that the content must satisfy, data types governing the content of elements and attributes, and more specialized rules such as uniqueness and referential integrity constraints.

For even more refined constraints, there is a dedicated schema language called Schematron. For example, it can require that the content of an element be controlled by one of its siblings. Or that an element must have specific attributes. Or that an attribute must have certain, possibly conditional, values. Schematron can also specify required relationships between multiple XML files and be used to create "plain-English" validation error messages rather than the usual cryptic ones. [Schematron](http://schematron.com/) is an ISO recommendation, standardized by ISO/IEC FDIS 19757-3.

It is possible to insert Schematron in ODD files (and hence RELAX NG files). Like the schema, the schematron must be declared in the root element. It looks like this:
```xml
TEI@xmlns:sch="http://purl.oclc.org/dsdl/schematron"
```
TEI itself uses Schematron to declare restraints on many of its tags.

## Do it yourself

By default, all Brill XML files that are TEI P5 compliant are associated with a TEI P5 schema. This happens in the root element, and looks something like this: `<TEI xmlns:rng="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei\_all.rng">`. The schema takes the form of a RELAX NG file (Brill's preferred format) and lives on the TEI servers. The advantage is that there is no need to store a validation file in the same location as the xml file. Also, Brill staff doesn't need to worry about having the latest version. TEI takes care of that.

It is also possible to reference the schema in one of the other formats. (Use `TEI@xmlns:xsd` for Schema, and `<!DOCTYPE TEI SYTEM "https://www.tei-c.org/release/xml/tei/custom/schema/dtd/tei\_all.dtd">` for DTD). Alternatively, you can download the schema and reference it locally.

The tei\_all.rngschema validates against all of TEI, as the name indicates. Use Roma to create schemas with a more narrow scope.

Lastly, the website _TEI by Example_ has an online validator especially for TEI XML. Paste chunks of codes or entire documents here: [http://teibyexample.org/xquery/TBEvalidator.xq](http://teibyexample.org/xquery/TBEvalidator.xq). Its error messages are a little more user-friendly than that of most parsers.

## Recommendation

Further analyze and apply schema and Schematron in order to enforce editorial guidelines and enhance data quality.
