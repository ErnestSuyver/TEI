## Epidoc

### Background
As remarked above, the TEI Guidelines offer an encoding scheme for a wide range of texts. Encoders will therefore have to choose, and these Brill Guidelines offer the Brill scheme. Such adaptation is called "customization". TEI actively supports customization through guidelines and formal mechanisms.

One type of text is formed by _inscriptions_. In the Classics community, a TEI customization has been developed to deal specifically with (predominantly) Greek and Latin inscriptions. It is called _Epidoc_.

(Note that Brill uses a DTD which is called "TEI Epidoc". This proprietary and idiosyncratic validation schema has little more in common with this customization than the name).

### Guidelines

This customization has its own [website](https://sourceforge.net/p/epidoc/wiki/Home/).

### Explanation

First off: think of Epidoc as the XML equivalent of the Leiden Conventions. The Leiden Conventions – or simply "Leiden" – are a set of marks specifically for the scholarly edition of epigraphic and papyrological texts. See  [https://en.wikipedia.org/wiki/Leiden\_Conventions](https://en.wikipedia.org/wiki/Leiden_Conventions).

This set has been subject to variety and different interpretations. The table below details the Leiden conventions as they are currently used in one of Brill's MRWs (abbreviated as "SEG"). Expect this list to change over time.

### Leiden and Epidoc

#### SEG inscription text in Epidoc


| Nr  | Description | SEG | EpiDoc | Render as |
|---|------|------|-------|----- |
| II | Line breaks | n/a | `<lb n="1"/>first line<lb n="2"/>second line` | New line (preceded by line number every five lines) |
| -- | Word divided across lines | αβγ-δεζ | `<lb n="1"/>αβγ<lb n="2" break="no"/>δεζ` Add hidden text here? I've also seen `<lb type="worddiv">` | Hyphen to indicate word break |
| -- | Text divisions | n/a | `<div type="textpart" subtype="face" n="r">…</div><div type="textpart" subtype="face" n="v">…</div>` | ? |
| III.1 | Clear text | αβ | αβ | αβ |
| III.2 | Clear but incomprehensible letters | ΑΒ | `<orig>αβ</orig>` | ΑΒ |
| III.3 | Letters ambiguous outside of their context | α̣β̣ | `<unclear>αβ</unclear>` | α̣β̣ |
| III.4 | Vestiges of letters visible but illegible | ... | `<gap reason="illegible" quantity="3" unit="character"/>` | ... |
| III.5 | Text visible to previous editor, but now lost | n/a | `<supplied reason="undefined" evidence="previouseditor">αβγ</supplied>` | ? |
| -- | Text restored by comparison with parallel copy | n/a | `<supplied reason="undefined" evidence="parallel">αβγ</supplied>` | ? |
| IV.1 | Apices | n/a | `<hi rend="apex">a</hi>` etc. | ? |
| IV.2 | Supralinear lines | n/a | `<hi rend="supraline">abc</hi>` | ? |
| IV.3 | Claudian letters | n/a | Unicode characters: Ⱶ, Ↄ, Ⅎ |   |
| IV.4 | Ligatured letters | n/a | `<hi rend="ligature">ab</hi>` | ? |
| V.1 | Erased | ⟦αβ⟧ | `<del rend="erasure">αβ</del>` | ⟦αβ⟧ |
| V.3 | Erased and lost | ⟦...⟧ | `<del rend="erasure"><gap reason="lost" quantity="3" unit="character"/></del>` | ⟦...⟧ |
| VI.1 | Text struck over erasure |  n/a | `<add place="overstrike">αβγ</add>` | ? |
| -- | Erased and overstruck or corrected | n/a | `<subst><del rend="corrected">αβ</del><add place="overstrike">γδ</add></subst>` | ? |
| VII.1 | Text added by ancient hand (above?) | n/a | `<add place="above">αβ</add>` | ? |
| VII.1 | Text added by ancient hand (below) | n/a | `<add place="below">αβ</add>` | ? |
| VIII.1 | Characters lost but restored | \[αβ\] | `<supplied reason="lost">αβ</supplied>` | \[αβ\] |
| -- | Characters restored tentatively | \[αβ?\] | `<supplied reason="lost" cert="low">αβ</supplied>` | \[αβ?\] |
| -- | Word incompletely restored | ἑτα\[ῖρ-\] | `<w part="I">ἑτα<supplied reason="lost">ῖρ</supplied></w>` | ἑτα\[ῖρ-\] |
| VIII.2 | Characters lost, lacuna | \[...\] | `<gap reason="lost" quantity="3" unit="character"/>` | \[...\] |
| VIII.3 | Lacuna, extent unknown | \[----\] | `<gap reason="lost" extent="unknown" unit="character"/>` |   |
| -- | Lacuna, approximate extent |   | `<gap reason="lost" quantity="5" unit="character" precision="low"/>` | ? |
| VIII.4 | Lacuna, praenomen | n/a | `<name><gap reason="lost" atLeast="1" atMost="3" unit="character"/></name>` | ? |
| -- | Lacuna, range of possible extent | n/a | `<gap reason="lost" atLeast="5" atMost="7" unit="character"/>` | ? |
| VIII.5 | Line lost | n/a | `<gap reason="lost" quantity="1" unit="line"/>` | ? |
| VIII.6 | Line(s) lost at start or end of text | n/a | `<gap reason="lost" extent="unknown" unit="line"/>` | ? |
| VIII.7 | Line possibly lost | n/a | `<gap reason="lost" quantity="1" unit="line"><certainty match=".." locus="name"/></gap>` | ? |
| VIII.7 | Line(s) possibly lost at start or end of text | n/a | `<gap reason="lost" extent="unknown" unit="line"><certainty match=".. " locus="name"/></gap>` | ? |
| IX.1 | Superfluous letters; suppressed by editor | {αβ} | `<surplus>αβ</surplus>` | {αβ} |
| IX.2 | Omitted letters; added by editor | `<αβ>` | `<supplied reason="omitted">αβ</supplied>` | `<αβ>` |
| IX.3 | Letters corrected by editor | `<αβ>` | `<choice><corr>αβ</corr><sic>βα</sic></choice>` | `<αβ>` |
| -- | Word regularized by editor | n/a | `<choice><reg>ἐκ</reg><orig>ἐγ</orig></choice>` | ? |
| X.1 | Expansion of abbreviation | α(βγ) | `<expan><abbr>α</abbr><ex>βγ</ex></expan>` |   |
| -- | Tentative expansion of abbreviation | α(βγ?) | `<expan><abbr>α</abbr><ex cert="low">βγ</ex></expan>` |   |
| -- | Incomplete expansion of abbreviation | α(βγ-) | `<w part="I"><expan>α<ex>βγ</ex></expan></w>` | α(βγ-) |
| -- | Incomplete expansion (Duke) | n/a | `<expan>α<ex>βγ </ex></expan>` | ? |
| X.2 | Abbreviation: expansion unknown | n/a | `<abbr>α</abbr>` | ? |
| X.3 | Expansion of symbol | (αβ) | `<expan><ex>αβ</ex></expan>` | (αβ) |
| X.4 | Subaudible word supplied by editor | n/a | `<supplied reason="subaudible">αβγ</supplied>` | ? |
| X.5 | Text not completed by stonecutter | n/a | `<gap reason="omitted" extent="unknown" unit="character"/>` or `<gap reason="omitted" extent="unknown" unit="line"/>` | ? |
| XI.1 | Editor's note, i.e. 'sic' | n/a | `<note>!</note>`, `<note>sic</note>`, `<note>e.g.</note>` | ? |
| XI.2 | Space left on stone | v. or vacat | `<space quantity="1" unit="character"/>` | v. or vacat |
| XI.3 | Space on stone, extent unknown | vac. | `<space extent="unknown" unit="character"/>` | vac. |
| XI.4 | Words omitted by editor for brevity | n/a | `<gap reason="ellipsis"/>` | ? |
| -- | Direction of text | ™ | `<lb n="1" rend="right-to-left"/>` | ™, but ideally text direction |
| -- | Numeral (Roman) | n/a | `<num value="12">XII</num>` | ? |
| -- | Numeral (Greek) | α' | `<num value="1">α</num>` | α' |
| -- | Symbol | ((leaf)) or leaf | `<g type="leaf"/>` | ((leaf)) or leaf |

Warning. There is, it seems, not _one_ Leiden system, but many. This may be due to the differences in interpretation and application, or differences between Greek and Latin epigraphy. Below are a few examples of marks which are supposedly Leiden but have so far has not found a place in Epidoc.

| sign | description | 
|-----|-----|
| ì | I longa |
| âb | letters joined together in a nexus | 
| - - - - - - | loss of complete lines but their precise number cannot be ascertained |
| `<<abc>>` | letters inscribed in an erasure |
| ⌜abc⌝  | etters erroneously inscribed, but corrected by the editor | 
| D •M •s | interpunction between words or letters | 
| ⸦columba⸧  | image inserted into the inscription and described by the editor, commonly using Latin words | 

These examples are taken from Christer Bruun and Jonathan Edmondson edd., _The Oxford Handbook of Roman Epigraphy_ (2014). ISBN: 9780195336467. DOI: 10.1093/oxfordhb/9780195336467.001.0001.

#### Epidoc in XML
The list above focuses on editorial signs. These are applied to the inscription text. Or rather, to the transcription of that text. This transcription sits in an `<ab>` element within a `<div>` element. The latter has a number of specific attributes that _must_ occur:

```xml
<div type="edition" xml:space="preserve" xml:lang="grc-Grek" n="some_CTS_or_CITE_URN">
```

The `<ab>` contains numbered lines, i.e. `<l>` elements with an `@n` attribute

```xml
<ab>
    <lb n="1"/>Greek or Latin (etc.) text here
</ab>
```

When an inscription consists of multiple parts, each parts sits in its own `<ab>` and has `@type` with the value "textpart" and `@n` with the name indicating the text part (often A, B, C or I, II, III). See [http://www.stoa.org/epidoc/gl/latest/trans-textpart.html](http://www.stoa.org/epidoc/gl/latest/trans-textpart.html) which seems to offer a choice between `<ab>` and `<div>`.

#### Non-textual information

Inscriptions can present crowns, leaves, and other non-textual features. How to deal with them? One option is to take them as a character, and specific their type. Thus: `<g type="coronis-lower-half"/>`. See [here](http://aquila.zaw.uni-heidelberg.de/paptrac/wiki/gtypes) for an example, as well as Nicola Reggiani, _Digital Papyrology I: Methods, Tools and Trends_. Another approach is to take them as a text part. This allows for the insertion of text in the text part, as in this example where the text is inscribed over the crown: `<div type="textpart" subtype="corona" n="cor.1"><ab><supplied reason="lost">ὑπὸ Τυρανῶν</supplied></ab></div>`. See [http://iospe.kcl.ac.uk/1.30.html](http://iospe.kcl.ac.uk/1.30.html), with an illustration of an inscription with coronae available at [http://iospe.kcl.ac.uk/iip/iipsrv.fcgi?FIF=inscriptions/10.22.jp2&amp;CVT=jpeg](http://iospe.kcl.ac.uk/iip/iipsrv.fcgi?FIF=inscriptions/10.22.jp2&amp;CVT=jpeg).

#### Other text

Critical apparatus, translation, commentary, and bibliography can be placed in `<div>` elements with relevant `@type` attribute values.

#### Photographs

Epidoc XML files allow for the insertion of a `<facsimile>` element between the `<teiHeader>` and `<text>` elements, where a photograph of the stone can be referenced with `graphic@url`.

#### Metadata

Another major feature of the Epidoc customization is the use of the teiHeader to store information about the stone on which the inscription is present. There are many tags for information about location and date and for detailed description of the stone and the inscription itself. Too many to mention here – see the example of the SEG template below for an impression.

#### Validation

Validate against the TEI Epidoc Customization Schema – called _tei-epidoc.rng_ – by adding the following between the XML declaration and the root element:

```xml
<?xml-model href="http://www.stoa.org/epidoc/schema/latest/tei-epidoc.rng" schematypens="http://relaxng.org/ns/structure/1.0"?>
<?xml-model href="http://www.stoa.org/epidoc/schema/latest/tei-epidoc.rng" schematypens="http://purl.oclc.org/dsdl/schematron"?>
```

#### Example - template

The so-called "SEG template" shows a selection of Epidoc elements to encode a Brill MRW in the field of epigraphy. The template itself has no content; it only shows the fields. It can be found here: `G:\Publishing Projects\ARC\CLS\3 Major Works\_MRWs\SEG\SEGO\8. SEG Forward\SEG_Forward_editing_environment_and_database\XML Template\SEG Forward Generic Template.xml`.

#### Example

Below follows an example of the transcription or edition of an inscription (in this case iSEG 63 369) in Leiden and in Epidoc.

_Leiden_
```
--------------------
v. ΤίτϽ Φλάβιον Ἀλέ-
4 v. ξανδρον τὸν σο-
v. φιστὴν [- -] ΦλάϽ Φοῖνιξ
[- - - -]
καὶ Φύλαξ τὸν πατέ-
v. ρα (etc.)
```

_Epidoc_
```xml
<gap reason="lost" extent="unknown" unit="line"/>
<lb n="3"/><space quantity="10" unit="character"/>Τίτ<hi rend="superscript">Ͻ</hi> Φλάβιον Ἀλέ
<lb n="4" break="no"/><space quantity="4" unit="character"/>ξανδρον τὸν σο
<lb n="5" break="no"/><space quantity="4" unit="character"/>φιστὴν <gap reason="lost" quantity="2" unit="character"/> Φλά<hi rend="superscript">Ͻ</hi> Φοῖνιξ
<lb n="6"/><gap reason="lost" extent="unknown" unit="character"/>
<lb n="7" break="no"/>καὶ Φύλαξ τὸν πατέ
<lb n="8"/><space quantity="4" unit="character"/>ρα <note>etc.</note>
```

#### Epigraphic resources

- [I.Sicily](http://sicily.classics.ox.ac.uk/). Project to make freely available the complete corpus of inscriptions from ancient Sicily, in all languages across all of antiquity. See also the [blog](https://isicily.wordpress.com/)

#### Epigraphic databases

- [Epigraphische Databank Heidelberg](http://edh-www.adw.uni-heidelberg.de/home). Contains the texts of Latin and bilingual (i.e. Latin-Greek) inscriptions of the Roman Empire.
- [Trismegistos](https://www.trismegistos.org/index.html). An interdisciplinary portal of papyrological and epigraphical resources formerly Egypt and the Nile valley (800 BC-AD 800). [https://www.trismegistos.org/index.html
- [PHI](https://inscriptions.packhum.org/). Searchable Greek Inscriptions from the _Packard Humanities Institute_.

#### Epigraphic tools

- [Epidoc GitHub](https://github.com/EpiDoc)
- [Epidoc Cheatsheet](https://svn.code.sf.net/p/epidoc/code/trunk/guidelines/msword/cheatsheet.pdf)
- [Epidoc Guidelines](http://www.stoa.org/epidoc/gl/latest/)
- [Wikipedia entry on Epidoc](https://en.wikipedia.org/wiki/EpiDoc)
- [Wikipedia entry on the Leiden system](https://en.wikipedia.org/wiki/Leiden_Conventions)
- [Overview of resources](https://warwick.ac.uk/fac/arts/classics/postgrads/modules/epigraphy/bibliog/online/)
- [Another overview of resources](http://www.saxa-loquuntur.nl/)

