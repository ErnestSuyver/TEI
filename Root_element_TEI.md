# Root element TEI

## Background

Every TEI file consists of a metadata section and a text section. Both sections are contained within one element, the very first element of every TEI file: the root element `<TEI>`.

## Guidelines

See the [TEI Guidelines](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-TEI.html).

## Explanation

The mandatory root element `<TEI>` has attributes instructing the parsers which namespaces occur in the document and which schemas to use for validation. First, the TEI namespace http://www.tei-c.org/ns/1.0 is declared, using the `@xmlns` attribute. Then, the document is associates with two schemas, RelaxNG and Schematron, using the `@xmlns:rng` and `@xmlns:sch` attributes, so its structure can be validated. The `@xmlns:xs` attribute proved some extra information about the schema. The `@xmlns:type` attribute provide the media type application (registered with IANA, RFC 6129) enabling  automated recognition and processing of TEI files by external applications.

Another attribute, and of a different character, is `@xml:id` which identifies the XML file. (Or the text it contains, no such distinction is presently made).

The root element is preceded by the XML declaration. This specifies the version number of the XML Recommendation applicable to the file (in our case, version 1.0) and the character encoding (in our case, UTF-8).

A word about the encoding: `@encoding="UTF-8"` means that the 16-bit characters of Unicode have been mapped to UTF-8, which uses one to four 8-bit bytes to encode all of the 1,112,064 valid code points in Unicode. TEI XML works with Unicode, but the representation of TEI XML in a parser requires a font (or character set), and not all fonts contain all characters. In such cases, it can be helpful to represent such characters as character references in the hexadecimal notation, e.g. &amp;#x00E9; for é. The underlying character encoding for XML is the same. For that reason, there is no need to declare such references in a schema.

There is a small set of character entity references that do not have to be declared either because they form part of the definition of XML. These include characters that have a specific use in XML, such as the opening and closing angle brackets, the ampersand and the double and single quotations marks. Use of such entities might confuse parsers: is it xml or content? To disambiguate, these entities are "escaped", i.e. noted as predeclared entity names: `&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&apos;` respectively.

The XML declaration is purely documentary, but if it is wrong many XML-aware processors will be unable to process the associated text.

There are many ways to encode the information required in the root element and the XML declaration, and this is the Brill way. It is recommended to use them as they are. Exceptionally, there may be situations in which they need to be changed, particularly if a different way of validation is required. See the section on validation elsewhere in this manual.

## Example
```xml
<?xml version="1.0" encoding="UTF-8"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0"
     xmlns:rng="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei\_all.rng"
     xmlns:sch="http://purl.oclc.org/dsdl/schematron"
     xmlns:xs="http://relaxng.org/ns/structure/1.0"
     xmlns:type="application/tei+xml"
     xml:id="COM-00001">
```

## Recommendation

The value of `TEI@xml:id` is supposed to identify the _file_ `1872-5309_ewic_fulltextxml_COM-00001.xml`, for example. But this file has a non-unique value COM-00001 in the `@xml:id` attribute in its root element. This may lead to confusion. Replace this value with the unique `a10.1163_1872-5309_ewic_COM_00001`.
