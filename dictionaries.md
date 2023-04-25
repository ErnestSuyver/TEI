## Dictionaries

### Background

Brill publishes are great number of dictionaries, some as monographs, others as reference works. Some bear the word "dictionary" in their title, like _The Brill Dictionary of Ancient Greek Online_, others words like "Lexicon" or "Concordance", others are harder still to recognize. Many dictionaries can be found on [http://dictionaries.brillonline.com/](http://dictionaries.brillonline.com/), some on [http://chinesereferenceshelf.brillonline.com/](http://chinesereferenceshelf.brillonline.com/), and others on [Brill Online Reference Works](https://referenceworks.brillonline.com/subjects) or [Brill.com](brill.com).

No systematic approach to structuring ("tagging") the content has been applied so far. These guidelines aim to change that, using the TEI standards and best practices as a reference point.

### Guidelines

TEI discusses dictionaries in [Chapter 9 Dictionaries](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DI.html). As always: TEI offers a wealth of options, so Brill chooses what is pertinent, based on concrete cases. It is perhaps good to add that TEI should not be taken as a _tag set_ but as a _model_ for structuring content. TEI helps us analyze content: this is the basis for any structuring, in XML or whatever medium.

### Explanation and examples

The *structure* may very per dictionary. Let's leave aside front and back matter and subdivisions for the moment and focus on the *entry*. (TEI often supposes that the electronic version wants to preserve the print features. However, _online_ this does not always make sense; also, there is a difference between making an electronic facsimile of a dictionary and transforming a dictionary into a digital publication environment). The semantics of the entry may, again, differ per dictionary. For example, some dictionaries may provide distinct entries for homographs, other may combine them. However, typically an entry contains a *headword*, i.e. some morphological form of the lexical item described, is sorted in some meaningful order (alphabetical or otherwise), and is divided into senses (or subsenses). This gives us the following basic structure:

```xml
<entry>
    <form>
        <orth></orth>
    </form>
    <hom n="1">
        <sense n="1"></sense>
        <sense n="2"></sense>
        <!--  etc. etc. -->
    </hom>
</entry>
```

For the sake of consistence, it might be prudent to use `<hom>` even if there is only one homograph.
Let's now take a closer look at the entry structure. Entries can contain different bits of information about a lexical entity, called "top-level constituents" in TEI speak. These include:

- information about the form of the word treated (orthography, pronunciation, hyphenation, etc.)
- grammatical information (part of speech, grammatical sub-categorization, etc.)
- definitions or translations into another language
- etymology
- examples
- usage information
- cross-references to other entries
- notes
- related entries

This gives us the following more complex structure:

```xml
<entry>
    <hom>
        <form>
            <orth></orth>
            <gramGrp>
                <pos></pos>
            </gramGrp>
        </form>
        <sense>
            <def></def>
            <cit>
                <quote></quote>
            </cit>
            <usg></usg>
            <xr></xr>
            <etym></etym>
            <note></note>
            <re></re>
        </sense>
    </hom>
</entry>
```

Of course, this is an artificial example; in reality, there will be more information, and the sequence of tags will be different.

### Applying CTS, CITE, and CapiTainS

There is no point in repeating the [Brill CTS Guidelines](https://brillpublishers.gitlab.io/documentation-dts/) here. Instead, we give a summary:

- entries and senses get a CITE URN
- citations get a CTS URN (or CITE URN when not taken from a canonical text)

_Entries_ belong to the physical structure of a dictionary. THey are objects in a collection. For purposes of referencing, they need to receive a CITE URN. There can also be other identifiers:

- Entry ID. Mandatory. Value of `entry@n` or `@xml:id`. This is the CMS record ID if the entry was created in a CMS. It can also be a CITE URN. If CMS ID and CITE URN are both used, the latter may be a value of `anchor@n`, which is added immediately after the `<entry>` tag. Example: `<anchor n="urn:cite:brill:lgo.ger:01_1208"/>` 
- There may be an additional identfies, such as a DOI if the entry is  be published as an independent publication unit. In such cases, the optional attribute `@sameAs` is used.

_Senses_ belong to the logical structure of the dictionary. They can be connected to texts and corpora, as annotations. For such purposes, they need to receive a CITE URN. So, a sense has a

- CITE URN. Mandatory. Value of `anchor@n`, which is added immediately after the `<entry>` tag. Example: ```<sense n="1"><anchor n="urn:cite:brill:lgo.ger:ἀντίϑεσις.1"/>```

Likewise, a subsense has

- CITE URN. Mandatory. Value of `anchor@n`, which is added immediately after the `<entry>` tag. Example: ```<sense n="a"><anchor n="urn:cite:brill:lgo.ger:ἀντίϑεσις.1.a"/>```

Citations receive a CTS or CITE. To be precise:

- CTS or CITE URN. Mandatory. Value of `ref@target`, which is wrapped around the `<cit>` element that wraps the `<quote>` and `<bibl>` tags

For example: 
```xml
<ref target="urn:cts:brill.bra00010.brw00001.296.11"><cit type="example"><quote xml:lang="grc-Grek">ἐπεὶ οὖν τῷ ἀληϑῶς ἀγαϑῷ πρὸς τὸ μή άληϑῶς ἀγαϑόν έστιν ἡ ἀ., ἀμεσος δὲ τῶν δύο τούτων ἡ έναντίωσις</quote><bibl>34,34,9</bibl></cit></ref>
```

