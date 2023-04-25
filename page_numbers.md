## Page numbers

### Background

For Brill MRWs, the XML files are often used as the source of both print and online publications. In print, page numbers make sense. In online, less so, because of unpredictably changing screen sizes. Nonetheless, it can be necessary to display page numbers online, for example if the print was published first and the page numbers are part of canonical references. Usually, it is not possible to add page numbers during the content creation process and they have to be included after typesetting.

### Guidelines

There is no chapter on page numbers in the TEI Guidelines. There is [Chapter 11 Representation of Primary Sources](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/PH.html), which offers some advice on page numbers, but in a slightly different context than that of Brill MRWs. The most relevant section is [Chapter 3.10.3 Milestone Elements](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#CORS5).

### Explanation

In TEI, milestone element mark elements that do not form part of the primary structural hierarchy. For example, a collection of poems may have a primary structural hierarchy of collection-poem-stanza-line. This structure does not necessarily correspond to a grammatical structure of sentences and clauses, as a line may contain more or less than one sentence. In such cases, milestone elements are used to mark the sentences. The same applies to scholarly texts, where lines are usually considered to be a (typographical) feature of a particular (print) edition rather than a structural characteristic.

The milestone element for pages is `<pb/>` in TEI. It is a closed element, but can take an `@n` attribute to encode the page number. Remember that "pb"  stands for page beginning, not page break, meaning it should be placed ahead of the page it is indicating. `@place` and `@type` are also perfectly acceptable attributes. Brill also uses the `@ana` attribute to encode the volume number. Lastly, `@ed` is used to indicate the work containing the pages.

For the sake of completeness, here are some other milestone elements: `<lb/>`, the line beginning which we already encountered in the section on verse; `<cb/>` or column beginning (which may be encountered in the less fortunate form of `pb@corresp` in Brill TEI XML files); `<gb/>` or gathering beginning, something that applies to the transcription of codices; and the neutral `<milestone>`.

### Example
```xml
<pb ed="ASD" ana="4" n="60"/>
```

<!-- 
### Note about milestone elements
Milestone elements derive their name from the `<milestone>` element. Milestone elements are **empty** but can have attributes for additional information.

Element | Description
----- | ------
`<milestone>` | any beginning
`<gb>` | gathering beginning
`<pb>` | page beginning
`<cb>` | column beginning
`<lb>` | line beginning
-->

### Milestone elements 

* Tag one structure of the text with `<div>` and other elements, like `<l>`. This may be the _logical_ structure of the text, but it could also be a dominant physical structure. 
* Tag the _other_ structure(s) with a milestone element, to wit `<milestone>`
* We use `<l>` instead of `<lb/>`, even in prose etc. This is because we need to unambiguously indicate the span of the line, and because milestone elements are closed so cannot sit in the middle of an x-path.
* we only use `<milestone>` but not the other milestone elements
* There are four **mandatory** attributes of `<milestone>`:
  * @unit. The value is **always** "section".
  * @ed. The value is the name of the edition or the name of the editor.
  * @type. The value is free.
  * @n. The value is free, but usually a number.

#### Example

```xml
<milestone ed="Wiston" type="chapter" unit="section" n="1" />
```

<!--
**Suggestion**. Tag the _dominant_ structure of the text with `<div>` and other elements, like `<l>`. This tends to be the _logical_ structure of the text. Tag the _other_ structure(s) with milestone elements. Use attributes to identify the structures. (These tend to be the _physical_ structures).

**Question**. Which milestone elements should be used to identify the alternative structures? Only `<milestone>` itself, unless others are absolutely necessary? What about `<lb>`? I'm not sure the idea of prefacing a line in a text edition with `<lb>` was a good one, because we really need an end tag... 
-->





