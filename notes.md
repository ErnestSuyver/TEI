## Notes

### Background

A note is any additional comment found in a work, yet separate from the base text. Such notes can be found at the foot of a page (footnotes), or at the end of a chapter or monograph (endnotes). A critical apparatus, though separate from the base text, is hardly additional and hence not usually regarded as a set of notes. Commentaries or translations that are complete separate from the base text – e.g., published in a separate volume – are not regarded as notes either. Marginalia, on the other hand, usually are.

One might call a note a type of annotation. An annotation is any text that bears a relation to another. There is overlap between text reuse (relation of repetition) and annotation.

Characteristic of notes, at least in scholarly texts, are their marks of attachment to the base text: often a number, sometime a letter or other symbol.

### Guidelines

See TEI Guidelines [Chapter 3.8 Notes, Annotation, and Indexing](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CONO).

### Explanation

Brill uses the TEI element `<note>` to encode the notes in its publications. The position of the note is encoded in the `@place` attribute, which may have values like "foot", "end", and "margin". There is some potential overlap here with `@type`, so use "gloss", "translation", "comment", etc. as type values. Remember that TEI intends such values to represent the position of notes in a source text that is being digitized. Brill, on the other hand, uses these values to instruct applications – such as typesetting systems or online publication platforms – as to the desired position of these comments.

Footnote numbers have two functions: they visually mark where base text and note are attached and they identify the note. For example, a sentence in the base text make conclude with a superscript number "six", which number might be found at the foot of the page identifying the sixth note of the page or chapter. Such a number is stored in the `@n` attribute. (TEI allows non-numerical values here too, so a dagger or letter are perfectly acceptable).

Lastly, there are two possibilities that TEI offers that Brill doesn't use at the moment, but which could prove highly useful. The first is marking a span of attachment rather than a point. A point is just that: a single location where a note marker is found. It does not give precise information about which section of the base text is commented on in the note. Yet this is exactly what a span does. There are numerous ways to do this; the simplest is to use a `<seg>` with some `@xml:id` and have the note refer to the span using `@target` (which then takes the value of the `seg@xml:id` as its value). By the way, there are ways to deal with overlapping spans in TEI, but this is not the place to explain them.

The second possibility is to store the note separate from the base text. The default position is at the point of attachment. There is no default way of grouping notes; a `<div>` with `@type` and some relevant value will do. Again, use a reference to connect note and point (or span) of attachment, e.g. with `<seg xml:id="n007" type="noteAnchor">` in the base text and somewhere else `<note target="n007">`. The advantage is a more easily readable base text and the option of grouping multiple sets of notes.

### Example
```
<p>And yet it is not only in the great line of Italian renaissance art, but even in the painterly <note place="bottom" type="gloss"><term xml:lang="de">Malerisch</term>. This word has, in the German, two distinct meanings.</note> style of the Dutch genre painters...</p>
```

### Recommendation

1. Always number the notes. This guarantees that in every version and every medium or format, the note numbers are the same. Do not rely on automatic numbering by the platform (as is presently often the case). Remember that `@n` numbers notes and `@xml:id` identifies the `<note>` element. This is not the same.

2. Use note numbers that are absolutely unique. Not `n="6"`, but `n="_2452-4107_thb_COM_0006020100_note_06"`, for example.

