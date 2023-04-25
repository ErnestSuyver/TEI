## Languages and scripts

### Background

Identification of language and script is a crucial requirement to a specialized humanities publisher like Brill. Only a correct identification can lead to the display of the correct characters in the correct glyph in the correct font in print and online.

Brill uses the values listed under [BCP-47](https://tools.ietf.org/html/bcp47) to identify the _language_. A 'BCP' is a best current practice, which is a document by the _Network Working Group_ of the _Internet Engineering Task Force_. BCP-47 is based on the [IANA language registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry), which in its turn is based in the [ISO 639](http://www.iso.org/iso/catalogue_detail?csnumber=39534) standard for (two-character and three-character) language identifiers. See also [this](https://www.loc.gov/standards/iso639-2/php/code_list.php) useful overview.

Brill uses the values listed under [ISO 15924](https://www.iso.org/standard/29546.html) to identify the _scripts_. This list can also be found at the [Unicode site](http://unicode.org/iso15924/iso15924-codes.html).

### Guidelines

See [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CH.html#CHSH](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CH.html#CHSH)

### Explanation

Brill uses the TEI attribute `@xml:lang` to identify language and script. The value of the attribute is a pair of language and script identifiers. This sentence, for example, which is written in (modern) English in the Latin script, can be tagged as `@xml:lang="en-Latn"`.

Brill requires _all_ language and scripts to be identified. Of course, many Brill MRWs are written in English, with pockets of other languages and scripts. In TEI XML, there is no need to tag every sentence. The tag can be applied to the highest possible level, as kind of default value pair, and only the exceptions then need to be noted explicitly. This can be quite complex, though, as different languages and scripts mingle, especially if the writing direction also changes.

In TEI XML, the values of `@xml:lang` refer to the BCP-47 language (and script) identifiers that are declared in the document's metadata. We already encountered this in the section on the `<profileDesc>` element. The `<teiHeader>` contains a `<profileDesc>` which may contains a `<langUsage>` element. This element may contain one or more `<language>` elements describing the languages, registers, dialects, etc. that occur in the text. The `<language>` elements take an `@ident` attribute to identify the language. The values of this attribute are taken from BCP-47. Here, too, we see the linking mechanism described in the section on references.

It may be that typesetters, when creating print PDFs in TeX or InDesign, or publication platforms, when rendering codes into human-readable fonts and characters, act directly on the values of `@xml:lang`. However, without `<langUsage>`, the XML would not be valid and no application would parse it. So while language and script are marked wherever they occur, the codes used in these marks are declared in the metadata.

`@xml:lang` is a global attribute in TEI. This means it can be attached to any TEI element. The main consideration in this application is, therefore, clarity: is the text in a given language unambiguously identified as such? Sometimes, it is clear: a quotation contain text in Portuguese and nothing else can be tagged as `<quote xml:lang="pt-Latn">`. If a tag contains multiple languages, or if a tag contains content in one language *as well as* a tag with content in another language, then the `<foreign>` element can be used to attach `@xml:lang` to. For example, instead of `<p>The Portuguese word fundadores has four syllables.</p>`, use `<p>The Portuguese word **<foreign xml:lang="pt-Latn">**fundadores<foreign> has four syllables.</p>`.

### Explanation of other language properties

In the context of writing, language and script are not the only relevant factors. _Writing direction_ (or 'directionality') is another one. Latin script runs from left to right for example, but Arabic from right to left. This directionality is included in the Unicode characters that encode the script. However, some characters have "weak" directionality, i.e. they run in the direction of the writing surrounding them. This is not always the desired behavior. Think of symbols used in text editions: these may be in the Latin script, whereas the text is in Hebrew; thus, they would change direction and even be displayed at the wrong end of a phrase. Obviously this problem occurs when different scripts are mixed. (Note that not all scripts have fixed directionality: for example. the Greek script can run left to right, but also alternate direction per line, in boustrophedon text).

To prevent this, Brill has adopted a belt-and-braces method that explicitly states the directionality in addition to the Unicode points and the `@xml:lang` value pairs. This is done in two ways using the `@style` attribute with a CSS value pair:

1. `@style="direction: ltr"` or `style="direction: rtl"`
2. `@style="unicode-bidi: isolate"`

Whereas the first `@style` value pair is straightforward, the second demands explanation. "Unicode-bidi" refers to the Unicode Bidirectional Algorithm. See this [technical report](http://unicode.org/reports/tr9/) by the Unicode consortium. It defines a number of rules enabling software to render sequences of characters which have differing directionality properties in a predictable and reliable way, using only those properties. However, as we saw above, situations may rise where this approach results in ambiguity or lack of precision. The Unicode algorithm uses "isolates" to enforce the directionality of a given character independently of its surroundings. (Or rather, these characters thus become "isolates").

The default CSS value pair for directionality is `@style="Unicode-bidi: normal"`. There seems little point in including it; it is mentioned for the sake of completeness only. However, `@style="Unicode-bidi: isolate"` is relevant, as it prevents ambiguities or parts of a document being displayed in unexpected ways. For a more detailed discussion, see the W3C Internationalization Working Group report _Inline markup and bidirectional text in HTML_, at [https://www.w3.org/International/articles/inline-bidi-markup/#where](https://www.w3.org/International/articles/inline-bidi-markup/#where).

In short, these CSS value pairs ensure that the observed directionality of the text is unambiguous, even if TEI considers them superfluous.

The above pertains to _horizontal_ directionality. There is also _vertical_ writing direction. It this is made explicit in the CSS value pairs, a third factor needs to be included. This is the direction in which glyphs in a line, lines in a block, and blocks in a sequence are arranged: from top to bottom, from right to left, or left-to-right. The CSS value – the value of the `@style` attribute – thus becomes a triple. For English, for example, we might find `@style="writing-mode: horizontal-tb"`, whereas Japanese has `@style="writing-mode: vertical-rl"` and Mongolian `style="writing-mode: vertical-lr"`.

Another relevant factor is _alignment_. This alignment in the sense of vertical justification of text blocks. It is a consequence of directionality. Again, `@style` is used to trigger the CSS, using three value-pairs: "text-align: left", "text-align: center", and "text-align: right".

One more relevant factor is _rotation_. Again, CSS values do the trick: `@style="transform:rotateY(45deg)"` and similar commands. More explanation of these features is not warranted by the scope of the current MRW content. The challenge here is not to incorporate TEI P5 tags, but to get the CMSs to insert them and to get the CMSs, typesetters, and platforms to display them.

A final relevant factor is _text orientation_. This concerns the rotation of glyphs. When vertical and horizontal scripts are mixed, for example in a French-Chinese or Japanese-Indonesian dictionary, the need may arise to make explicit how the glyphs are oriented. The table below gives the pertinent CSS value pairs.

### Text orientation

| **TEI P5** | **Annotation** |
| ----- | ----- |
| style="text-orientation: mixed" | Default. Specifies that characters from horizontal-only scripts are set sideways, i.e. 90° clockwise from their standard orientation in horizontal text. Characters from vertical scripts are set with their intrinsic orientation. |
| style="text-orientation: upright" | Specifies that characters from horizontal-only scripts are rendered upright, i.e. in their standard horizontal orientation. Characters from vertical scripts are set with their intrinsic orientation and shaped normally. |
| style="text-orientation: sideways-right" | Causes text to be set as if in a horizontal layout, but rotated 90° clockwise. Vertical orientation in horizontal scripts. |
| style="text-orientation: sideways-left " | Causes text to be set as if in a horizontal layout, but rotated 90° counter-clockwise. Vertical orientation in horizontal scripts. |
| style="text-orientation: sideways" | [https://www.w3.org/TR/css-writing-modes-3/](https://www.w3.org/TR/css-writing-modes-3/) |
| style="text-orientation: use-glyph-orientation" | [https://www.w3.org/TR/css-writing-modes-3/](https://www.w3.org/TR/css-writing-modes-3/) |

### Example
```xml
<p>Examples include Jer 21:2 (<foreign style="direction:rtl; unicode-bidi:embed;" xml:lang="he-Hebr">נְבוּכַדְרֶאצַּרמֶלֶךְ־בָּבֶל</foreign> "Nebuchadrezzar, king of Babylon" instead of βασιλεὺς Βαβυλῶνος "King of Babylon") and Jer 26[33]:22 (<foreign style="direction:rtl; unicode-bidi:embed;" xml:lang="he-Hebr">הַמֶּלֶךְיְהֹויָקִים</foreign> "Jehoiachim, the king" instead of ὁ βασιλεὺς "the king").</p>
```

### Appendix on glyph variants

Unicode makes possible the use of the correct character, but the glyph is chosen (or set) by the font. However, in some cases it may be required to display a glyph variant. There is Brill documentation on the fonts containing the glyph variants, on the Open Type functionality that enables this, and on the input and display of such glyph variants. It remains here to show how this works in TEI XML.

The key is BCP-47, which allows more values than only language and script. In this case, we add to the value an "x" to indicate private use, followed by the identifier of the glyph variant. This is added to the element surrounding the character of which we want the glyph variant to be displayed. Brill requires that a glyph variant is set per individual character. Therefore, the element must be `<g>`, which stands for "gaiji", which is the Japanese term for a non-standardized character or glyph. The XML will thus read
```xml
<g xml:lang="[language id]-[script id]-x-[glyph variant id]">[Unicode point]</g>
```
Note that this use of the `<g>` element is not standard TEI: TEI would have a `@ref` attribute in `<g>` with a value that refers back to declared characters (or glyph variants) in a `<charDecl>` element in the `<encodingDesc>` element.
