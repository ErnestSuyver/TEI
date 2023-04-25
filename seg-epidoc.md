## Epidoc

* Epidoc is XML for inscriptions and papyri, a customization of TEI
* _TEI Epidoc_ XML is created at [export](https://github.com/BrillPublishers/SEGAdmin/wiki/Serverside-functionality#export)
* There is a template for what the XML should look like

# XML Template for SEG entries
The SEG Forward Generic Template for XML is found here:

> G:\Publishing Projects\ARC\CLS\3 Major Works_MRWs\SEG\SEGO\8. SEG Forward\XML Template\SEG Forward Generic Template.xml

and looks like this:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <?xml-model href="http://www.stoa.org/epidoc/schema/latest/tei-epidoc.rng" 
    schematypens="http://relaxng.org/ns/structure/1.0"?><!-- epidoc -->
    <?xml-model href="http://www.stoa.org/epidoc/schema/latest/tei-epidoc.rng" 
    schematypens="http://purl.oclc.org/dsdl/schematron"?><!-- epidoc -->
    <TEI xmlns="http://www.tei-c.org/ns/1.0"
   xmlns:rng="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng" 
   xmlns:sch="http://purl.oclc.org/dsdl/schematron" 
   xmlns:xs="http://relaxng.org/ns/structure/1.0" 
   xmlns:type="application/tei+xml" 
   xml:id="some_id"><!-- SEG entry ID -->
   <teiHeader xml:lang="en">
      <fileDesc>
         <titleStmt><title level="a"></title>
            <author ref="VIAF URN">
               <name type="person"><persName><surname></surname><forename></forename></persName></name>
               <idno type="ORCID"/>
               <idno type="ISNI"/>
            </author>
            <funder ref="placeholder"/>
         </titleStmt>
         <publicationStmt>	
             <authority>Supplementum Epigraphicum Graecum</authority><!-- epidoc -->	
             <idno type="URI">CTS_CITE_URN</idno><!-- inscription id  --><!-- epidoc -->
             <idno type="localID">human_readable_ID</idno><!-- epidoc -->	
             <idno type="filename">file_name</idno><!-- epidoc -->	
             <idno type="recource"></idno><!-- epidoc -->
            <publisher>BRILL</publisher>
            <pubPlace>Leiden | Boston</pubPlace>
            <availability status="restricted">
               <licence target="https://creativecommons.org/licenses/by-sa/4.0/">Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)</licence>
            </availability>
            </publicationStmt>
         <sourceDesc>
             <msDesc><!-- epidoc -->	
	                    <msIdentifier>
	                        <country>museum country</country>
	                        <region>museum country</region>
	                        <settlement>museum place</settlement>	
	                        <repository role="museum" ref="Museum URI">Museum Name</repository><!-- current location, unless it is in the field  -->
	                         <idno type="inventory_number">inventory number</idno>
	                        <altIdentifier>
	                            <settlement/>
	                            <repository/>
	                            <idno type="old"/>
	                        </altIdentifier>
	                    </msIdentifier>
	                    <physDesc>	
	                        <objectDesc>
	                            <supportDesc>
	                                <support>description of object/monument (likely to include <material/>
	                                    and <objectType/> information, <dimensions/>, etc.)</support>
	                            </supportDesc>
	                            <layoutDesc>
	                                <layout>description of text field/campus</layout>
	                            </layoutDesc>
	                        </objectDesc>
	                        <handDesc>
	                            <handNote>description of letters, possibly including <height>letter-heights</height>
	                            </handNote>
	                        </handDesc>
	                    </physDesc>
	                    <history>
	                        <origin>
	                            <origPlace><placeName ref="Pleiades URN">Place of origin</placeName></origPlace><!-- place of origin -->
	                           <origDate notBefore-custom="number" notAfter-custom="number" precision="medium" datingMethod="#julian" period="some_URN" when="0001-01-01">date/century/period</origDate><!-- date  -->
	                        </origin>
	                        <provenance type="found">Findspot and circumstances/context</provenance><!-- finding place  -->
	                        <provenance type="observed">Modern location(s) (if different from repository, above)</provenance><!-- current location, unless it is in a museum -->
	                    </history>
	                </msDesc>
            <bibl>
               <title level="m">Supplementum Epigraphicum Graecum</title><!-- series -->
               <editor><!-- editor -->
                  <persName>
                     <forename></forename>
                     <surname></surname>
                  </persName>
               </editor>
               <biblScope unit="volume"></biblScope><!-- volume -->
               <biblScope unit="entry"></biblScope><!-- entry -->
               <idno type="DOI"></idno><!-- DOI -->
               <idno type="sams-id"></idno>
               <idno type="publisher-id"></idno>
               <idno type="ISSN"></idno>
                <idno type="seg:entry:type"></idno><!-- entry type  --><!-- here we deviate from the other tei files at brill -->
            </bibl>
         </sourceDesc>
      </fileDesc>	
      <profileDesc>
         <abstract><p/></abstract>
          <calendarDesc><!-- epidoc -->
                <calendar xml:id="julian">
                    <p>Julian Calendar</p>
                </calendar>
            </calendarDesc>	
         <langUsage>
            <language ident="en"/>
             <language ident="grc-Grek"/>
         </langUsage>
         <textClass>
             <keywords scheme="brill:subject"><!-- here we deviate from the other tei files at brill -->
               <term>Classics</term>	
            </keywords>
             <keywords scheme="http://www.eagle-network.eu/voc/typeins.html"><!-- inscription type  --><!-- epidoc -->
                 <term ref="some_URI">some term</term>
             </keywords>
             <keywords scheme="seg:selected-topics"><!-- Selected topics -->
	<term xml:lang="en">some term</term>
	</keywords>
             <keywords scheme="seg:names"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
             <keywords scheme="seg:kings"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
             <keywords scheme="seg:emperors"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
             <keywords scheme="seg:geography"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
             <keywords scheme="seg:military"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
             <keywords scheme="seg:religous"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
             <keywords scheme="seg:important-words"><!-- index term type -->
                 <term xml:lang="grc">some term</term><!-- index term -->
             </keywords>
         </textClass>
      </profileDesc>
      <encodingDesc>
          <refsDecl n="CTS"><!-- Capitains Guidelines -->
              <cRefPattern 
                  n="level1"
                  matchPattern="(\w+)"
                  replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div/tei:div[@n='$1']">
                  <p>This pointer pattern extracts inscriptions (and new readings)</p>
              </cRefPattern>
              <cRefPattern 
                  n="level1"
                  matchPattern="(\w+)"
                  replacementPattern="#xpath(/tei:TEI/tei:text/tei:body/tei:div/tei:div[@n='$5']">
                  <p>This pointer pattern extracts comments</p>
              </cRefPattern>
              </refsDecl>
         <styleDefDecl scheme="css" schemeVersion="3.0"/>
         <tagsDecl>
            <rendition xml:id="italic">font:italic;</rendition>
            <rendition xml:id="bold">font:bold;</rendition>	
            <rendition xml:id="underline">font:underline;</rendition>
            <rendition xml:id="subscript">font:subscript;</rendition>
            <rendition xml:id="superscript">font:superscript;</rendition>
            <rendition xml:id="smallcaps">font:smallcaps;</rendition>
         </tagsDecl>
      </encodingDesc>
      <revisionDesc>
         <change when="20180101" status="print"/><!--publication year SEG  --><!--  the alternative is to use <date> in <publicationStmt> -->
         <change when="20190101" status="correction" who="#Chaniotis"/>
      </revisionDesc>		
   </teiHeader>
    <facsimile>
        <graphic url="photograph of text or monument"/>
    </facsimile>
    <text>
        <body>
            <div type="edition" xml:space="preserve" xml:lang="grc-Grek" n="some_CTS_URN"><!-- language  --><!-- inscription text  --><!-- epidoc --><!-- Capitains Guidelines; use if epidoc -->
                <ab>
                    <lb n="1"/>Greek or Latin (etc.) text here
                </ab>
            </div>
            <div type="apparatus"><!-- apparatus criticus --><!-- epidoc -->
                <listApp>
                    <app loc="some-part_and_line_number"><!-- use @loc only when there is a reference to a line number... -->
                        <note></note>
                    </app>
                </listApp><!-- the alternative is a simple <p> -->
            </div>
            <div type="translation"><!-- epidoc -->
                <p>translation(s)</p>
            </div>
            <div type="commentary" n="some_URN"><!-- Summary  --><!-- group description; if from-to entry type  --><!-- Capitains Guidelines; use if tei --><!-- if tei, also add @xml:lang -->
                <head></head><!-- heading  -->
                <p>commentary
                    <note></note><!--  Notes  -->
                </p>
            </div>
            <div type="bibliography"><!-- Bibliographic data; uitwerken  -->
                <bibl></bibl>
            </div>
        </body>
    </text>
</TEI>
```

## Some examples of the XML for the different `biblType`
**article in journal**
```xml
<biblStruct>
           <analytic>
              <author ref=""><forename></forename><surname></surname></author>
              <title level="a"></title>
              <idno type="DOI"></idno>
           </analytic>
           <monogr>
              <title level="j"></title>
              <imprint>
                 <pubPlace></pubPlace>
                 <date></date>
              </imprint>
              <biblScope unit="volume"></biblScope>
              <biblScope unit="page"></biblScope>
              <biblScope> <idno type="ISSN"></idno></biblScope>
           </monogr>
        </biblStruct>
```

**chapter in monograph**
```xml
<biblStruct>
           <analytic>
              <author ref=""><forename></forename><surname></surname></author>
              <title level="a"></title>
              <idno type="DOI"></idno>
           </analytic>
           <monogr>
              <editor ref=""><forename></forename><surname></surname></editor>
              <title level="m"></title>
              <imprint>
                 <pubPlace></pubPlace>
                 <date></date>
              </imprint>
              <biblScope unit="page">
                 <idno type="ISBN"></idno>
                 <!-- <idno type="DOI"></idno> -->
              </biblScope>
           </monogr>
        </biblStruct>
```
**monograph**
```xml
<biblStruct xml:id="">
            <monogr>
               <author ref=""><forename></forename><surname></surname></author>
               <title level="m"></title>
               <imprint>
                  <pubPlace></pubPlace>
                  <date></date>
               </imprint>
               <biblScope>
                  <idno type="DOI"></idno>
                  <idno type="ISBN"></idno>
               </biblScope>
            </monogr>
         </biblStruct>
```
**edition**
```xml
<biblStruct xml:id="">
            <monogr>
               <editor ref="#COM-00021"><forename></forename><surname></surname></editor>
               <title level="m"></title>
               <imprint>
                  <pubPlace></pubPlace>
                  <date></date>
               </imprint>
               <biblScope>
                  <idno type="DOI"></idno>
                  <idno type="ISBN"></idno>
               </biblScope>
            </monogr>
         </biblStruct>
```

## Some more details
## Date
* We decided against a separate object for date
* Instead, the date properties are now properties of `inscription`.
* They are `date_label`, `date_period_id`, `date_notBefore`, `date_notAfter`, `date_when` and `date_precision`.
* it is still an open question if we should have something like `create @cert=”low”` or a field to store stuff like "c." and "about"
* it is still an open question if we should have radio button for BC and AD in the interface.
* These properties look as follows in TEI Epidoc:
```xml
<origin>
  <origDate notBefore-custom="number" notAfter-custom="number" precision="medium" datingMethod="#julian" period="some_URN" when="0001-01-01">date/century/period</origDate>
</origin>
```
