## Text editions and critical apparatus

### Background

Text editions are often conceived of as the construction of an ideal or original text out of a number of variant texts. Such editions are scholarly because they present these variants and justify a choice or suggested reading. The critical apparatus is where this justification takes place, as annotations to a base text.

Today, there is increasing interest in the variants themselves as relevant objects of scholarly analysis. (Scribal "errors", for example, can tell us much about the scribe's linguistic environment). This reverses the relation between base text and critical apparatus. The latter is no longer solely an annotation, but a container of variants, from which any of these variants can be generated, as well as a preferred text.

If properly encoded, a critical apparatus can fulfil both requirements. Likewise, the base text must meet certain requirements for scholarly use, such as the representation of linear, hierarchical, and other structures. See also the Brill CapiTainS Guidelines.

### Guidelines

The relevant place in the TEI P5 Guidelines is [Chapter 12 Critical Apparatus](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/TC.html). As always, TEI offers a host of options. For reasons of simplicity and uniformity, Brill has made a selection on the basis of concrete needs.

#### Explanation – base text

As explained in the section on reference structures, TEI expects the XML structure of an encoded text to follow the logical structure of that text. The choice of elements depends on the type of text. The `<div>` and `<ab>` elements may be appropriate for prose, the `<lg>` and `<l>` elements for verse. Remember that `<p>` and `<lb/>` elements are used to encode typographical features, and therefore belong to the non-logical (in this case, physical) structure of a text.

Note, lastly, that TEI offers a multitude of ways to encode manuscripts in order to create a digital facsimile. However, this is not relevant to Brill at this moment. While Brill publishes digital facsimiles as part of primary source collections, they are currently not encoded in TEI. The focus of this section is therefore on critical text editions.

#### Explanation – critical apparatus

In TEI, a critical apparatus is a formal and structured way of collecting variants of a text. It may contain a list of witnesses: texts that testify of a given variant. The element `<witness>` records the witness; a `<listWit>` element contains multiple of such recordings. A `<witness>` element may contain information about the manuscript, printed edition, translation, or quotation that provides the text variant, in prose or in a `<bibl>` element. It must have an `@xml:id` attribute, because that is used in pointers in the critical apparatus proper. The list of witnesses is placed in the same XML file that contains the base text, following the CapiTainS guidelines, in a separate `<div type="witnesses">`.

Quick remark on the term "apparatus". Not every apparatus is critical. There can be anapparatus of citations or an apparatus of sources. "Apparatus" here means a body of (usually structured and formal) annotations. A criticalapparatus is a body of annotations concerning text variants.

Individual text variants are recorded in an `<app>` element. Usually, the variants are encoded in a `<rdg>` element, which stands for "reading". Thus an `<app>` may contain one or more readings of text. The `<rdg>` element must have a `@wit` attribute with a value that is identical to the value of the `@xml:id` attribute in `<witness>`. This is a variant of the pointer-anchor structure discussed in the section on references. To indicate of which term or phrase the variants are recorded, the `<lem>` element may be used, which again must have a `@wit` attribute.

A word about `<lem>`. The name of this element obviously refers to "lemma", which means headword or the uninflected variant of a term. Here, it may be used to mark unproblematic readings in witnesses, or to mark a scholar's preferred reading, or simply to mark the phrase in the text of which variant readings exist. A scholar may also decide not use it, if the idea of a "base", "original, or "unproblematic" text is not suitable. TEI offers no guidelines on the exact usage of this element or its contents. Encoders must pay close attention.

The `<lem>` element further raises the question of how to connect base text and critical apparatus, and where the place text-critical annotations. Starting with the latter: it is possible to insert an `<app>` element in a line of base text, or straight after it (after the `<l>` element). However, this leads to bloated text. Brill therefore prefers to place the `<app>` elements in a `<listApp>` element. This element is placed in the same XML file that contains the base text, following the CapiTainS guidelines, in a separate `<div type="critical apparatus">`. Multiple `<app>` elements can be gathered in a `<listApp>` element, and a `<div>` of the type "critical apparatus" may contain multiple `<listApp>` elements.

TEI offers three ways to connect base text and critical apparatus: (1) the location-referenced method; (2) the double-end-point attached method; and (3) the parallel-segmentation method. Method (3) is designed for text edition without a base text; so far Brill has not published those; it is therefore not covered here. Methods (1) and (2) rely on the encoding of a text's logical structure, a subject briefly discussed in the section on references. It basically works as follows: the structuring elements have an `@n` attribute. The values of these `@n` attributes are concatenated in the pointer of the `<app>` element. In this case, the pointer is a `@loc` attribute.

Usually, the deepest level is the line. This means the text-critical annotations are attached to the base text on line level. This is not unusual in text editions. The presence of `<lem>` can point the user to the exact location within the line. This method – which basically is method (1) above – is perfectly clear to humans; it has its origin in the world of print. However, it is not unambiguous, and so for cases where greater precision is required, method (2) is devised. This works by marking a span in the base text, which acts as an anchor – or rather, as a doublet of anchors: a beginning anchor and an end anchor – for the pointer in the critical apparatus. This is where the `<anchor>` element comes into its own, as it may be used for both beginning anchor and end anchor. (The matter of overlapping spans is too complex to be covered here).

Brill uses CTS URNs as identifiers in its text editions, as detailed in the Brill CTS/CITE/CapiTainS Guidelines. These offer the option to identify any location in a text, including ranges. This means that Brill can use method (1) _and_ still mark spans. The benefit of the simplicity of the location-referenced method is combined with the benefit of the precision of the double-end-point attached method.

Don't forget to state the method in the text's metadata: in the `<encodingDesc>` element in the `<teiHeader>`, place this empty element: `<variantEncoding method="location-based" location="external"/>`.

### Example

In this case, the witnesses are placed in a `<div>` inside the `<div>` with the critical apparatus. Other choices can be made.

Note that the second `<app>` contains a span.

```xml
… <teiHeader> … <encodingDesc><variantEncoding method="location-referenced" location="external"/>… </encodingDesc>… </teiHeader>
<text><body>…
    <div xml:lang="lat-Latn" type="edition" n="urn:cts:latinLit:stoa0023.stoa001.brill-lat1"><head>Ammiani Marcellini Rerum Gestarum libri qui supersunt</head>
    <div type="textpart" n="14" subtype="book"><head>Liber XIV</head>
    <div type="textpart" n="1" subtype="chapter"><head>Galli Caesaris saevitia</head>
    <div type="textpart" n="1" subtype="section">
        <p>Post emensos insuperabilis expeditionis eventus, languentibus partium animis, quas periculorum varietas fregerat et laborum, nondum tubarum cessante clangore… </p>
    … </div>…</div>…</div>…</div>…
    <div type="witnesses"><head>Index siglorum</head>
        <listWit>
            <witness xml:id="a">[manuscript a]</witness>
            <witness xml:id="b">[manuscript b]</witness>
            <witness xml:id="c">[manuscript c]</witness>
            <witness xml:id="d">[manuscript d]</witness>
        </listWit>
    </div>
    <div type="critical_apparatus">
        <listApp>
            <app loc="urn:cts:latinLit:stoa0023.stoa001.brill-lat1:14.1.1@emensos">
                <lem wit="#a #b #c">emensos</lem>
                <rdg wit="#d">enensos</rdg>
            </app>
            <app loc="urn:cts:latinLit:stoa0023.stoa001.brill-lat1:14.1.1@languentibus-:14.1.1@animis">
                <lem wit="#a #b #d">languentibus partium animis</lem>
                <rdg wit="#c">om. c</rdg>
            </app>
        </listApp>
    </div>
</body></text>…
```

#### Recensions

Recension is the revision a text based on critical analysis, either by a contemporary scholar, or in the past. (Sometimes the word is also used for the construction of a stemma, i.e. an overview of textual transmission in the form of a tree structure). Such revision is handled in the critical apparatus. But what if there are multiple recensions? How to deal with this in TEI?

Recensions are handled in the base text, not in the apparatus. For example: there are three witness to a text:

* witness A: "…it's been the ruin of many a poor by…"
* witness B: "…it's been the ruin of many a poor girl…"
* witness C: "…it's been the ruin of many a poor girls girl"

Witness A represents recension I, witnesses B and C represent recension II. This is tagged as follows:

```xml
<p>… it's been the ruin of many a poor <choice><seg source="#recensio_1"><anchor xml:id="a1"/>boy<anchor xml:id="a2"/></seg><seg source="#recensio_2"><anchor xml:id="b1"/>girl<anchor xml:id="b2"/></seg></choice>…</p>
```

In the apparatus, there need to be separate `<app>` elements for #a1...#a2 and #b1...#b2.

```xml
<app from="#a1" to="#a2" ana="#recensio_1">
    <lem>boy</lem>
    <rdg wit="#A">by</rdg>
</app>
<app from="#b1" to="#b2" ana="#recensio_2">
    <rdg wit="#B">girl</rdg>
    <rdgGrp>
    <rdg varSeq="1" wit="C">girls</rdg>
    <rdg varSeq="2" wit="C"><subst><del>girls</del><add>girl</add></subst></rdg>
    </rdgGrp>
</app>
```

In the apparatus, the two readings of witness C are grouped in a `<rdgGrp>` element. The `@varSeq` attribute (variant sequence) gives a number indicating the position of this reading in a sequence, in this case first (1) girls, then (2) girl.

In the base text, the `<choice>` element groups _alternative encodings_ or _recensions_ for the same point in a text. ("Alternative" is not necessarily exclusive, it may be parallel). This is not the same thing as _multiple witnesses_ for the same point in a text. These are identified within an `<app>` element in the apparatus. A recension is more than a group of readings, as is illustrated by this example, where the lemma "boy" does not occur in any witness.

See also [https://en.wikipedia.org/wiki/Recension](https://en.wikipedia.org/wiki/Recension) and [https://blogs.library.duke.edu/dcthree/2018/01/10/digital-servius/](https://blogs.library.duke.edu/dcthree/2018/01/10/digital-servius/)

### Recommendation

As a publisher, Brill cannot decide how scholars craft their apparatus. Usually, digitization starts after submission of a manuscript or printed edition. However, we can express a preference: a preference for a _positive_ critical apparatus. This is a critical apparatus in which the reading of _each_ witness is explicitly mentioned in each `<app>` (even if the `<lem>` has a `@wit`). This has the advantage of precision. In a _negative_ critical apparatus, only witnesses with a reading differing from the lemma are explicitly mentioned. (Hence a `<lem>` will usually not have a `@wit`). Less information is given, so there is less opportunity to verify. Also, one can't know whether the information is omitted by the editor or by the witnesses. (The non-mentioned witnesses are by default supposed to be identical to the lemma). Greater precision in turn allows improved quality control. For example, a positive critical apparatus allows an automatic check if all witnesses (in the `<listWit>` element) do indeed occur in the `<app>` elements and vice versa.

