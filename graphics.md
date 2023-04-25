## Graphics (and other media)

### Background

While audio and video are not used often at the moment, images are widespread in Brill MRWs.

### Guidelines

See the TEI Guidelines [Chapter 3.9 Graphics and Other Non-textual Components](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#COGR).

### Explanation

Images in Brill MRWs often have information "baked in" so often the caption is not so much a concern as is the position, size, image quality, and whether it should be displayed in a lightbox ("pop-up"). Remember that the image itself – that is, a jpeg or mp3 file – is not stored in the XML, only a link to the file is.

In TEI, `<figure>` is the main element. It can contain `<head>` and `<figDesc>` elements for the caption and such information. Nested within is a `<graphic>` element and/or a `<media>` element. Brill uses these elements to indicate the location of the media file, with the `@url` attribute. (It is also possible, but not recommended, to place a `<desc>` in `<graphic>` and `<media>`). In the case of audio or video, Brill adds a `@mimeType` attribute to `<media>`, with value such as "audio/mp3" or "audio/wav". `<graph>` and `<media>` can take `@width`, `@height`, and `@scale` attributes to set display preferences. The lightbox function is triggered by a `@style` attribute with the value "display:popup". Unfortunately, this is not a correct CSS property-pair, but there is no other way.

### Example
```xml
<figure>
    <graphic url="bdr-vol1-p-109" style="display:pop-up"></graphic>
    <head>Grave Desecration Villaret</head>
    <figDesc>During the night of May 17, 1990, all of the graves were desecrated in the little Jewish cemetery of the Swiss village of Villaret.</figDesc>
</figure>
```

### Scholarly Editions

For publication of **online images** on SE, do as follows:

1. Check if images files have the correct names and formats
2. Place the images on `O:\` which is Brill's iiif service (images will be uploaded to the iiif server)
3. Check if @url in the CTS compliant TEI XML has the correct value

The correct value is `https://iiif.arkyves.org/image.jpg/full/500,/0/default.jpg`

For example `https://iiif.arkyves.org/LC2020_LHOM_01edition_RGB_L.jpg/full/500,/0/default.jpg`

The "500"  parameter sets the image width (relative to its full size). Replace "500," by "full" if you want to render the complete image.

#### Naming Conventions
Name the images as follows: `textgroup.work.version` followed by the extension

#### Formats
Allowed formats are `.jpg` and `.pgn`.

#### Other images
For images that are not inline (i.e, in the text), e.g. cover images in the Library (textgroup, work, version), edit the XM in the CTS files.

For example

```xml
<ti:work xmlns:cpt="http://purl.org/capitains/ns/1.0#"
   xmlns:saws="http://purl.org/saws/ontology#"
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:dct="http://purl.org/dc/terms/"
   xmlns:ti="http://chs.harvard.edu/xmlns/cts"
   xmlns:scm="http://schema.org/" 
   xmlns:scaife="https://scaife-viewer.org/" groupUrn="urn:cts:arabicLit:0668IbnAbiUsaibia" urn="urn:cts:arabicLit:0668IbnAbiUsaibia.Tabaqatalatibba" xml:lang="ar-Arab">
  <ti:title xml:lang="en-Latn">The Best Accounts of the Classes of Physicians</ti:title>
  <ti:edition workUrn="urn:cts:arabicLit:0668IbnAbiUsaibia.Tabaqatalatibba" urn="urn:cts:arabicLit:0668IbnAbiUsaibia.Tabaqatalatibba.lhom-ed-ara1" xml:lang="ar-Arab">
    <ti:label xml:lang="en-Latn">Edition</ti:label>
    <ti:description xml:lang="en-Latn">E. Savage-Smith, S. Swain, G.J. van Gelder eds., A Literary History of Medicine (Leiden 2020)</ti:description>
    <cpt:structured-metadata>
      <scaife:image>https://iiif.arkyves.org/LC2020_LHOM_01edition_RGB_L.jpg/full/500,/0/default.jpg</scaife:image>
   </cpt:structured-metadata>
   <!-- this is the cover image for the version -->
  </ti:edition>
  <cpt:structured-metadata>
      <scaife:image>https://iiif.arkyves.org/LC2020_LHOM_unit_RGB_L.jpg/full/full/0/default.jpg</scaife:image>
      </cpt:structured-metadata>
      <!-- this is the cover image for the text group -->
</ti:work>
```

!! not sure how to get an image for the work?? !!

### Recommendation

1. Use `@type` to distinguish (the presently undistinguished) different types of figures, such as illustrations, maps, or character images.

2. Similarly, distinguish different types of caption, using `<head>` for the name of the figure and `<figDesc>` for a description of the representation.

3. Images are a bit of an undeveloped area in MRWs. Redefine things like size, position, buttons, etc.

