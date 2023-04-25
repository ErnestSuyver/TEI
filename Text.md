# Text

## Background
The previous section on metadata has a structure that follows the sequence of elements in the `<teiHeader>`. The `<text>` element has no such sequence, because every text is different. The following sections are therefore given in random order.

## Guidelines
See TEI Guidelines Chapter 3 Elements Available in All TEI Documents, [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html), and 4 Default Text Structure, [http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DS.html](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DS.html).

## Explanation
The text or contents of the publication is encoded in the TEI `<text>` element. This is the second major part of any TEI document. It is in fact possible for a TEI document to group together several `<text>` elements, for instance when encoding an anthology. So far, this hasn't been the case for Brill MRWs. There are MRWs that combine several works, such as the collected works of an author. However, in such cases Brill follows the CapiTainS guidelines which prescribe one XML document per work.

The `<group>` option is not mentioned here of the sake of completeness, but to make the point that TEI was originally designed to encode existing publications, looking back as it were. This is not how one has to use XML, and it is not how Brill uses its XML. Brill uses its XML to look forward, to the publication that needs to be created form the structured content. TEI fully supports this use, and it simply means that not every element needs to be used by Brill.

A similar story applies to the `<text>` element. This can contain `<front>` and `<back>` elements for front and back matter, which Brill doesn't use because it has other mechanisms to ensure their creation. Brill does, however, use the mandatory `<body>` element.

Within the `<body>` element, one might find any number of elements, depending on the type of text that is encoded. A common tag is the `<div>` element, which stands for text division. Combine this with a `@type` attribute and a relevant value to mark the type of contents, such as  "commentary" or "bibliography".

Note that the `<p>` element, which stands for paragraph, is not a textual division but a typographical feature. So, while TEI is generally very free, and while it is well possible to have `<p>` within `<div>`, it is not possible to have `<p>` elements after `<div>` elements. Always place them within a structural unit.

A word about `<div>`. In the CMS, it is not possible to create new `<div>` elements. Therefore an entry will consist of a single `<div>`. Do we need more? We don't have a criterion for when to create new division. (This is different with other types of texts, such as text editions, where the `<div>` elements follow the logical structure of the text).

There are two exceptions to this rule. The CMS creates multiple `<div>` elements when it creates entries of the type "parent with children". Such entries incorporates other entries. These other entries have a `<div>` as body, and a `<div>` with metadata. The other exception is the bibliography (at the foot of an entry) which sits in a `<div type="bibliography">`.

Lastly a word about titles. TEI uses the `<head>` element for them. They can be placed straight in the `<body>` element, or within `<div>` elements or similar structural units.

