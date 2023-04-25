# Appendix on supplements

Brill wishes to be able to add supplements to MRW entries, as it does to journal articles and monographs. Supplements include media files, text files, and metadata.

Two scenarios are possible. (1) Publish supplements as open data, for example on the Figshare website, [https://figshare.com/](https://figshare.com/), where they are (collectively) identified by a DOI. (2) Lock the supplements behind a paywall. In that case, they are accessible via (the access management system of) the CCC platform, with the files residing in some media folder.

If supplements are present, they must be referred to in the TEI Header. Brill uses the `<notesStmt>` element for this purpose, which sits in `<fileDesc>`. It can contain one or more `<note>` elements, which may contain a `<ref>` element that references either a DOI or a media file. The `@type` attribute is used to distinguish between the two scenarios. Use the values "figshare" or "local". It is also possible to add text to the `<ref>`, for instance by adding a `<caption>` to an image containing an illustration.

## Example
```xml
<notesStmt>
    <note>
        <ref target="10.6084/m9.figshare.4725469.v1" type="figshare"></ref>
    </note>
    <note>
        <ref target="1568539x_148_09-10_s009_s0001.mp4" type="local"></ref>
        <caption>Paradise bird eating worms.</caption>
    </note>
</notesStmt>
```