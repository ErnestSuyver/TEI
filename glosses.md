## Glosses

### Background
Glosses are annotations to texts. In Classical Antiquity, terms or phrases in a text that were felt to require explanation were annotated with glosses; interlinear glosses in book rolls, marginal glosses in codices. Glosses could be compiled into texts of their own: glossaries. Dictionaries evolved from them. In printed texts, glosses were largely superseded by footnotes.

Glosses are important in Biblical Studies, Literature Studies, and Law. However, in the context of Brill publications and their digitization, glosses are most often used in Linguistics.

There are two main uses of glosses in linguistics: (1) a short annotation to a (possibly transliterated) term or phrase; (2) a longer and more structured annotation to a phrase or sentence, often with transliteration and translation, explaining not just the meaning of the phrase, but also its linguistic structure. This type is called "interlinear gloss" because it is structured by lines.

### Short glosses
How to tag this in TEI P5? Here is an example of a short gloss:
```
A Cossack longboat is called a _chaika_ 'seagull'.
```
This may be tagged like this:
```xml
A Cossack longboat is called a <hi rendition="#italics"><term>chaika</term></hi> '<gloss>seagull<gloss>'.
```
This tagging can be refined further: the `<term>` could receive an identifier to which the `<gloss>` could point, so that they are paired. Also, the presentation could be separate from the content, transferring the rendering of italics and quotation marks to the CSS. The result:
```xml
A Cossack longboat is called a <term xml:id="term1">chaika</term> <gloss target="#term1">seagull<gloss>.
```
An encoder might even regard "a Cossack longboat" as a gloss and tag it accordingly, using `@target` to connect it to _chaika_ and using `@n` to differentiate both glosses.

### Long glosses (interlinear glosses)
Here is an example of an interlinear gloss:
```
ni-c-chihui-lia                        in        no-piltzin        ce        calli

1sg.subj-3sg.obj-mach-appl        det        1sg.poss-Sohn        ein        Haus
```
Meaning: "I built a house for my son". This could be tagged by placing the first line with the source language in a `<term>` and the second line with the target language (i.e. translation) and grammatical information in a `<gloss>`. Clearly this is not a satisfactory solution. The very form of an interlinear gloss provides information that is not captured by such tagging. The vertical alignment between words or morphemes indicates a link; really a gloss in itself. The difference between the small capitals and the normal font (in the second line) tells us one is grammatical information (expressed formally), the other translation. Note furthermore that neither the source nor the target language is tagged; nor is the grammatical form (i.e. notation) declared.

### No standard
What does TEI make of this? TEI offers many options that are relevant to linguists, especially the chapters: Transcriptions of Speech (ch. 8), Dictionaries (ch. 9), Language Corpora (ch. 15), Simple Analytic Mechanisms (ch. 17), and Feature Structures (ch. 18). However, TEI offers no single solution. In fact, TEI is not widely used by linguists. They use a multitude of mark-up languages, offering solutions for interlinear glossed text (IGT), such as EMELD, ODIN, and EOPAS XML. Is it an option to use another mark-up language than TEI? (It's possible to incorporate other XML in TEI). No, because there is no single or simple solution for the tagging of IGT, neither in TEI nor in any other mark-up language. The main reason seems to be that linguists don't share a common set of methods. There is no conceptual model for IGT. The Leipzig Glossing Rules (LGR) that give many details for interlinear glosses are conventions, nothing more.

### Back to TEI
Can it be done at all in XML? The vertical alignment that is characteristic of IGL is the concern of a stylesheet (CSS). But it the concern of XML to structure IGL in such a way that this is possible. An additional concern is the capturing of semantic information. IGL might contain

- the source text or orthography
- a transliteration
- a phonetic transcription,
- a morphophonemic transliteration
- a word-by-word or morpheme-by-morpheme gloss, where morphemes within a word are separated by hyphens or other punctuation
- a translation, which may be positioned separate from the gloss if the source is too different to follow line by line

TEI seems to offers sufficient options to capture IGL in many aspects. For example:

```xml
<div type="source" xml:lang="es">
<p>
    <s xml:lang="es" xml:id="s1">
    <w xml:id="w1" lemma="no">No<fs><f name="part of speech" dcr:datcat="dc:1345" fVal="particle" dcr:valueDatcat="dc:1342"/><!-- ... --> </fs></w>
    <w xml:id="w2" lemma="me">me</w>
    <w xml:id="w3" lemma="decir"><m>dig</m><m>as</m></w>
    <pc>.</pc>
    </s>
</p>
</div>
<div type="translation" xml:lang="en">
    <ab>
        <s corresp="#s1">Don't tell me.</s>
    </ab>
</div>
```

This is a very simple example. It is easy to see how the mark-up soon gets heavily bloated as more annotations are added.

Is there a better way? We can regard IGT as multi-tier annotations: one morpheme with multiple annotations. It is possible to encode the source in one XML file, and the annotations in another. This is called stand-off annotation. TEI  has a mechanism for that. (It called "feature structures" and is in fact an ISO standard: ISO 24610-1:2006). However, the problem remains that this requires extensive tagging. It would have to be done by the author, because it requires expertise. However, Brill doesn't ask this of its authors, at the moment. We need a simpler solution.

We really only want to state that this is an interlinear gloss, that there is a source language and different types of annotations., and that we want to (vertically) align morphemes. Thus, the simplest possible XML would

- delineate IGT as such, e.g. in a `<div>` element with `@type="igt"`
- support additional information, e.g. `@xml:id`, `@xml:lang`, and `@src`
- define annotations, e.g. in an `<ab>` element with a `@type` attribute with relevant values, such as "meta", "utterance", "segmented" etc
- not bother alignment of words or morphemes as long as we use an unambiguous separator

The separator cannot occur in the contents of IGL; this includes for example spaces (u+0020) as LGR does not allow whitespace in the gloss, other than to indicate word boundaries (morpheme boundaries are to be expressed as hyphens).

### Workflow
The above attempts focus on XML. How to get there? How do linguists currently deal with IGT? What tools do they use to create, manage, process, and display IGT? This is a different approach: we establish what the input and output mechanisms require, and then work our way back to the XML.

Take the following workflow:

- Author creates IGT, either stand alone or as part of other content
- Author submits files
- Brill assesses technical correctness of files (e.g. is number of morphemes in gloss and segmented text is the same?)
- Author fixes technical problems.
- XML is produced (and published)

In the last step, an output mechanism can be used that linguists use.

### Input
Many linguists use specialized tools to create and manage IGT. Toolbox, for example, is widely used because of its automatic "parsing" functionality (i.e. morphological analysis). It also has a (relatively) widely used XML format. Other tools focus more on, say, aligning text to audio/video, or managing dictionaries, and have other XML formats (such as EOPAS, Transcriber, or ELAN). Linguists will often use several tools in the process of creating IGT. Given this variety, it makes sense for Brill to decide on a standard input format, and ask authors to submit in that format only.

Brill uses the tabular structure as standard. While it has the drawback that IGT has a tree structure rather than a tabular one, the advantage is that authors are familiar with it. (IGT data forms a tree:  one phrase is made up of many words, and each word can be several morphemes, and each morpheme may have several glosses. A translation usually follows the glosses, but it's better thought of as an annotation of the phrase than of words or morphemes). It's easy to envisage a table with a line per gloss; gloss types in the left column; one morpheme per column. For example:
```
A              B              C          D          E        F

meta           53;            ces;       Forkel (2015:311)

utterance      Pjdu           tam [      já         a        ty]

segmented      Pjdu           tam        já         a        ty

glossed        will.go.1SG    there      I          and      you

translation    You and I will go there.
```
It is well possible to generated structured data from a table, and do some automatic validation (e.g. does every column have a morpheme?). Problems for automatic processing are posed by the lack of a standard model (hence no standard labels or tagging) and the variable number of columns.

### Output
In linguistic applications, the EOPAS or ELAN representations are often used in the output of IGT. What tools are available in a more generic web context? Two candidates are _Leipzig.js_ and _Interlinear_. Both work roughly the same: the IGL is separate entity, as are the lines within it. They use space as a separator and rely on JavaScript and CSS for vertical alignment. They can be adapted to Brill use of XML. While tables (rendered from XML into HTML using CSS) may offer more possibilities, these tools offer the advantage of simplicity.

A combination of tables as input, simple XML in the middle, and these tools as output is also possible.

### Recommendation

1. Brill currently asks authors to submit interlinear glosses as tables. Provide `@type` to `<table>` and `<row>` to create unambiguous semantics.

2. Tables are labour intensive for Brill staff. Investigate simpler alternatives. Concentrate on Word as input location, than work forward to CMS, XML, and representation in print and online.

### See also

* Leipzig Glossing Rules: [http://www.eva.mpg.de/lingua/resources/glossing-rules.php](http://www.eva.mpg.de/lingua/resources/glossing-rules.php)
* Interlinear morphological glossing: [https://www.christianlehmann.eu/ling/ling\_meth/ling\_description/grammaticography/gloss/index.php](https://www.christianlehmann.eu/ling/ling_meth/ling_description/grammaticography/gloss/index.php)
* TEI for linguists SIG: [http://www.tei-c.org/Activities/SIG/TEI\_for\_Linguists/](http://www.tei-c.org/Activities/SIG/TEI_for_Linguists/) and [https://wiki.tei-c.org/index.php/LingSIG](https://wiki.tei-c.org/index.php/LingSIG)
* IGL markup: [http://tei-l.970651.n3.nabble.com/linguistic-interlinear-text-in-TEI-td4023787.html](http://tei-l.970651.n3.nabble.com/linguistic-interlinear-text-in-TEI-td4023787.html)  and [https://github.com/cldf/cldf/issues/10](https://github.com/cldf/cldf/issues/10)
* ODIN: [http://odin.linguistlist.org/](http://odin.linguistlist.org/) &amp; EMELD: [http://www.aclweb.org/anthology/U03-1008](http://www.aclweb.org/anthology/U03-1008) &amp; EOPAS: [http://www.eopas.org/help](http://www.eopas.org/help)
* Feature Structure annotation system: [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/FS.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/FS.html)
* Alignment benchmark: [http://alignments.lingpy.org/](http://alignments.lingpy.org/)
* Toolbox: [https://software.sil.org/toolbox/](https://software.sil.org/toolbox/)
* IGL in TeX: [https://www.ctan.org/tex-archive/macros/latex/contrib/gb4e](https://www.ctan.org/tex-archive/macros/latex/contrib/gb4e)
* ELAN: [https://tla.mpi.nl/tools/tla-tools/elan/](https://tla.mpi.nl/tools/tla-tools/elan/)
* Leipzig.js: [https://github.com/bdchauvette/leipzig.js](https://github.com/bdchauvette/leipzig.js)
* Interlinear: [https://github.com/parryc/interlinear](https://github.com/parryc/interlinear)
* James Tauber: [http://jtauber.com/blog/2006/01/28/dynamic\_interlinears\_with\_javascript\_and\_css/](http://jtauber.com/blog/2006/01/28/dynamic_interlinears_with_javascript_and_css/)

### Appendix
Specials is a short Unicode block allocated at the very end of the Basic Multilingual Plane, at U+FFF0–FFFF. Of these 16 code points, three are relevant in the context of glosses:

```
U+FFF9 INTERLINEAR ANNOTATION ANCHOR, marks start of annotated text
U+FFFA INTERLINEAR ANNOTATION SEPARATOR, marks start of annotating character(s)
U+FFFB INTERLINEAR ANNOTATION TERMINATOR, marks end of annotation block
```

