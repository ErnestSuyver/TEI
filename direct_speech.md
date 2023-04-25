## Direct speech and Performance texts

### Background

Performance texts include dramatic texts, screen plays,  and cinema or TV scripts. For Brill, dramatic texts are probably the most relevant, e.g. Greek tragedy or Humanist translations thereof. Performance texts may contain direct speech, and this text type can also be found in other texts relevant to Brill, such as Greek philosophical or literary works. For this reason, performance text and direct speech are covered together in this section.

### Guidelines

The basic explanation is given in TEI P5 Guidelines [Chapter 3.12.2 Core Tags for Drama](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CODR)) with in-depth coverage in [Chapter 7 Performance texts](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DR.html)).

As always, TEI  offers a host of options. For reasons of simplicity and uniformity, Brill choses a minimum number of generic elements based on concrete needs.

### Explanation

Performances texts are works and therefore have a logical structure. Given Brill's compliancy to CapiTainS, this means we use `<div>` to capture the logical structure of the body. Non-body elements, such as set information, records of performances, prologues and epilogues, and other front and back matter typically do not occur in Brill content so need not concern us here.

With one exception: the cast list. There is a dedicated elements for this, `<castList>` which contains one or more `<castItem>` with one or more `<role>`. Use `<role>` to describe the performing agent: the speaker or dramatic protagonist. Add `@xml:id` to identify the role; this captures marginalia identifying the speaker and allows for variation between, e.g., canonical and abbreviated forms.

We now turn to speech. Brill uses `<sp>` to indicate direct speech. If a `<castList>` is used, `<sp>` must contain `@who` to identify the role. The value of `sp@who` is therefore identical to that of `role@xml:id`. `<sp>` may contain a `<speaker>`. Use `<speaker>` to capture the speaker as they occur in the text. (This is not always the case, sometime hyphens or other typographical features are used to indicate speaker change).

The speech itself is captured in the `<sp>` tag in an `<ab>` if prose and `<l>` if non-prose (basically: any metrical or poetic text). `<p>` is also allowed for prose, but Brill reserves it for typographical paragraphs.

There is some overlap here with quotation. (See elsewhere in these Brill TEI Guidelines). Brill uses `<quote>` to indicate written passages cited from other works. Brill uses the `<said>` element for words or phrases represented as being spoken or thought by people or characters within the current work. We do this when in a work (usually prose) direct and indirect speech alternate. In other words: when a work contains _only_ direct speech, we use `<sp>`.

There is a potential complication when the line numbers of the direct speech or performance text do not tally with the line numbers of the text edition containing them. It is possible to combine `<l>` and `<lb/>`, each with their own `@n`. However, usually, this difference can be ignored and the edition line numbers taken as leading.

#### Example
```xml 
<div> …
    <castList>
        <castItem>
            <role xml:id="menae">** Menaechmus **</role>
        </castItem>
        <castItem>
            <role xml:id="penic"> Peniculus </role>
        </castItem>
    </castList>
    <sp who="#menae">
        <speaker>Menaechmus</speaker>
        <l>Responde, adulescens, quaeso, quid nomen tibist?</l>
    </sp>
    <sp who="#penic">
        <speaker>Peniculus</speaker>
        <l>Etiam derides, quasi nomen non noveris?</l>
    </sp>
    <sp who="#menae">
        <speaker>Menaechmus</speaker>
        <l>Non edepol ego te, quot sciam, umquam ante hunc diem</l>
        <l>Vidi neque novi; ...</l>
    </sp>
… </div>
```

