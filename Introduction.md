# Introduction

### XML

At the turn of the century, the idea of _XML first_ publishing arose. XML itself had been around since the 1980s. What was new was the idea that XML could be used for publication of the web. Indeed, people thought XML could be used for _anything_, could be used as a full-fledged programming language. That enthusiasm has waned as coding and web technologies have evolved rapidly and extensively in the ensuing decades. But the idea of  _XML first_ publishing remained. Let's examine it.

### why: pros and cons

...

### workflow

1. docx comes in
2. docx are ingested into editing system (usually InDesign)
3. edits are made (corrections, proofs, also editing, translating, indexing, etc.)
4. content is output into different formats, primarily PDF for print and PDF, XML for online publication.

Many variations are possible, e.g. the editing system is also the authoring system, meaning the authors write in the publisher's environment.

## TEI

<!--
Brill considers XML to be an essential part of its processes. For Major Reference Works (MRWs) – which form the subject of this document – XML is exported by the CMSs in which MRW content is created. Typesetters then process the XML to prepare a print publication; likewise, digital publication platforms process the XML to create an online publication. MRWs that are not created in CMSs – be they created in MS Word or originally published in print and now to be converted – likewise need to be encoded in XML.

Brill uses a variety of XML formats. In 2016, it was decided to use TEI conformant XML for those MRWs that were destined to migrate to a new publication platform, called _Content, Catalogue, and Corporate_ ("CCC" or "Triple-C"). It is hoped that the remaining MRWs will migrate, too, to a new platform for text editions. In that case, they, too, will be encoded in TEI conformant XML.
-->

TEI is the _de facto_ standard in the Humanities. TEI is not a standard like ISO. Rather, it is a vast body of knowledge, a pool of shared experiences regarding the digitization of texts – all manner of texts, including, but certainly not limited to, primary sources and scholarly publications. TEI is supported by a large community, both in academia and outside, and an infrastructure comprising a great number of tools and services.

TEI stands for _Text Encoding Initiative_, of which a central player is the TEI consortium that maintains  _guidelines_ and other documentation and resources. The main website of the consortium is [www.tei-c.org](http://www.tei-c.org/index.xml), where we read:

> The Text Encoding Initiative (TEI) is a consortium which collectively develops and maintains a standard for the representation of texts in digital form. Its chief deliverable is a set of Guidelines which specify encoding methods for machine-readable texts, chiefly in the humanities, social sciences and linguistics. Since 1994, the TEI Guidelines have been widely used by libraries, museums, publishers, and individual scholars to present texts for online research, teaching, and preservation. In addition to the Guidelines themselves, the Consortium provides a variety of [resources](http://www.tei-c.org/Support/Learn/) and [training events](http://members.tei-c.org/Events) for learning TEI, information on [projects using the TEI](http://www.tei-c.org/Activities/Projects/), a [bibliography of TEI-related publications](http://www.tei-c.org/Activities/SIG/Education/tei_bibliography.xml), and [software](http://www.tei-c.org/Tools/) developed for or adapted to the TEI.

The Guidelines are version P5 and can be found [online](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/index.html).

## This manual

XML is language. Like natural languages, it exists in many different formats. (Although these formats do have common denominators, unlike natural languages). Like natural languages, there are many different modes of expression. 

This is also the case for the XML language that is TEI. The "speaker" or rather, encoder, is free to express themselves. Yet this freedom is restricted by considerations of relevance and pertinence, and by the constrains that come with a language: the number of parts and the possibilities and impossibilities of their combinations.

TEI is vast, and so for encoded texts, a selection has to be made. These guidelines document this choice. The criteria of the selection are actual needs: situations that occur in Brill MRWs, i.e. challenges to the encoder. Note that TEI also offers the option to _extend_ the tag set. DO this when your text requires it. <!-- Brill has chosen _not_ to go down that road; it contravenes the goal of standardization.-->

These guidelines are not fixed. It is well possible that future MRWs pose new challenges, and that new choices need to be made: the addition of new TEI tags and mechanism, or the replacement of old ones. An understanding of the system or way of thinking behind TEI is therefore more important than a mechanical rehearsal of elements. These guidelines do address the system at times, but this understanding comes mainly through actual application of the TEI.

Lastly, encoders need to realize that XML has nothing to do with online publication (it far predates the web) and that TEI has nothing to do with XML. TEI is a body of knowledge expressing itself in XML simply because it is convenient. The relevance of TEI for Brill lies not in its tags, but in its way of thinking. It gives Brill conceptual tools to structure texts.

## For whom

This manual explains which elements and attributes may be used in text editions, out of the many possibilities that TEI offers. It elucidates how they may be used, and why, and gives examples.

It is aimed at anyone who deals with text editions: creators, editors, web people, folks interested in history, art, archeology...
<!--
It is aimed at colleagues who create and manage MRW content, typesetters who create printable files from MRW XML, CMS developers who build and maintain systems that export MRW XML, and platform developers who build and maintain systems that process MRW XML, and all others are interested in creating and processing structured content.

The advent of the CCC platform was the trigger to convert Brill content into widely used, standardized XML formats. For (most) MRWs, that meant TEI. The previous format was the proprietary "Encyclopaedia" DTD (ENC). This manual was written to guide the conversion from the old to the new XML format.
-->

The application of the TEI Guidelines is in no way a technical conversion process. It is the application of a way of thinking. TEI is a vast amount of opinions and experiences concerning text, structure, and digitization. It is imperative that all users of this manual get acquainted with this thought process.

A second point is that TEI is huge and therefore a selection needs to be made. The selection presented in this manual is based on current content and requirements, supplemented by a few requirements foreseen for the immediate future. Such a selection will always be too limited, too broad, and outdated as new requirements in new texts come up. The people and process that work with TEI XML will therefore need to look at the thought process (the 'why') rather than the selection (the 'what'). They can expect continuous change.

## These guidelines

These guidelines contain three main sections.

1. _Structure_. This is the main function of XML: to _structure_ the content. This section is by far the largest in these guidelines. It is split in three: metadata is detailed in the section on the "TEI Header", and the content itself in the section on "Text". A third section covers the subject of validation, i.e. the question of valid and well-formed XML.
2. _Meaning_. XML of the type used in TEI does _not_ convey meaning. Nonetheless, there is a need to include meaning and even a bare structure is not devoid of meaning. The main semantic vehicle is the `@type` attribute. (XML can be used to encode machine-readable meaning, but that is not in the scope of these guidelines).
3. _Presentation_. XML is built on "separation of concerns", where each layer does one job and one job only. So it is the job of XML to structure content, and the job of another layer to render (= display, represent) it. In the online world, that layer would be CSS working on HTML. In the world of print, it would be a PDF created by a typesetting program that does not usually have this separation. However, given that both act on the XML that Brill provides, and that Brill MRW staff need to style the contents as much as structure it, there was a requirement to include a mechanism for presentation in Brill's TEI XML. A major display vehicle is the `@style` attribute.

This list is not exhaustive. Another aspect is _functionality_. This is relevant in the context of online publication platforms, and specific to individual platforms. Therefore it is not covered here.

These guidelines conclude with a number of appendixes on pertinent subjects.

### Related documents

See the Guidelines on BPT and CTS.
