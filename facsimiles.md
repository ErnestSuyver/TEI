## Facsimiles

### Background

At the moment (Q4 2019) there is no facsimile proper on _Scholarly Editions_. But _DSS_ and _Brill325_ comes close.

### TEI
For publication of facsimile editions on [Scholarly Editions](https://dh.brill.com/scholarlyeditions/), CTS compliant TEI XML is required.

Let's start with the TEI. Let's assume a simple facsimile edition of manuscript, with an image and transcription for each page. In such a case, TEI advises to insert a `<facsimile>` element between `<teiHeader>` and `<text>`. This element basically contains a list of images, expressed in the form of closed `<graphic>` element, like this:

```xml
   <facsimile>
      <graphic url="page1.jpg" xml:id="page1"/>
   </facsimile>
```

The transcription of that page is found somewhere in `<text>`, for example in some `<div>`. The `<div>` has `@facs` attribute that refers back to the image, like this:

```xml
   <div facs="@page1">
      <ab>[transcription of page 1]</ab>
   </div>
```

This is a simple example. More complex ones will be added when required. Think of overlapping images, zones, ROIs or bounding boxes...

#### diplomatic
There are several types of transcription: diplomatic and normalized and what not. This is handled in the TEI XML. See the Guidelines.

### CTS
The basic idea is that image and text both represent an abstract object, e.g. a page in a printed book. The abstract page gets an identifier, and so do its manifestations. A single object can have many different manifestations: multiple images, multiple transcriptions, etc.

The object identifier needs to be a CITE URN. So does the image URN. Text has a CTS URN.

The abstract object URN gives us the manifestation URN, in CITE and in CTS (though there may be difference between them). Also, from the URN, the file name of the images and the xml ids (values of `@facs`) are derived.

#### An example:

Abstract page URN: 

`urn:cite:itaLit.AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v` 

Remember that this is the official CITE URN syntax: `urn:cite:citenamespace:collection.object@subreference`. For the sake of simplicity, in this example the CITE namespace is identical to the CTS namespace. The collection and object identifier are harder to distinguish because of all the full stops. Basically, the collection is `AntonioVallisneri.PrimiItinerisSpecimen` and the object is `folio.IV.v`. 

A concrete page URN would be:

`urn:cite:itaLit.AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1` 

However, this is no used (at least so far...). Instead, we use the identifier of the image in the XML: 

`AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1`

and this, really identical, file name:

`AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1.jpg`

Note the presence of the version identifier `eos-lat1`. 

### Some practical points regarding workflow:

#### git
A facsimile edition is a git repo like any other. Place it under _Data_ in Brill's GitLab. Do this **only** for the XML, following the CapiTainS guidelines. There is no need for version control on the images, therefore they don't go into git.

#### hotfolder
Place the images in the hotfolder G:\iiif (= O:) and they will be transported to the iiif server.

#### file names
The iiif server is one large name space. No folders or subgroups. Therefore, the file names of the images need to contain all information we need. We follow CTS, so this is the syntax of a file name:

`textgroup.work.version.extension`

For example: `AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1.jpg`

We cannot have semicolons in a file name, or other signs that make an operating system unhappy. Full stops are ok, so we'll have plenty of them.

What if we have groups of images? For example thumbnails and large images, or infrared ones? This information needs to go into the version identifier too. 

For example: `AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos.infrared-lat1.iri`

#### xml facs attribute
The value of `@facs` has to start with `#`. It makes sense to make the rest of the ID identical to the file name, and to the urn.

#### xml url attribute
The value of the `@url` attribute of `<graphic>` is identical to the filename. It is not a URL or path.

### TEI Guidelines
Chapter on representation of primary sources: https://www.tei-c.org/release/doc/tei-p5-doc/en/html/PH.html

### See also
* Facsimile and Document-Centric Editing: https://www.digitalmanuscripts.eu/wp-content/uploads/sites/6/2017/09/05-Digital-Facsimiles-EP.pdf
* ncoding guidelines for manuscript transcription: http://driscoll.dk/fasnl/FASNL_text_v1_2016.html
* TEI Boilerplate: Displaying a facsimile beside a transcription: https://tags.hypotheses.org/60 (edited) 
* a useful tool for annotation in TEI on images: http://teicat.huma-num.fr/zoner.php
* inspirational site: DTA. I admire their approach and execution. Look here for example: http://www.deutschestextarchiv.de/book/show/nn_oktavgfeo79_1828
* https://www.tei-c.org/release/doc/tei-p5-doc/en/html/PH.html
* https://andrewdunning.ca/transcribing-medieval-manuscripts-tei
* https://cmohge1.github.io/lrbs-digital-editing-intro-2019/TEI-documentary-transcription.pdf
* https://slides.com/jamescummings/tei-for-primary-sources/fullscreen#/
* https://github.com/oxygenxml/TEI-Facsimile-Plugin
* https://raw.githubusercontent.com/oxygenxml/TEI-Facsimile-Plugin/master/addon/image-markup-plugin.xml
* http://cite-architecture.org/imagemodel/


### Longer example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng" type="application/xml" schematypens="http://relaxng.org/ns/structure/1.0"?>
<?xml-model href="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng" type="application/xml" schematypens="http://purl.oclc.org/dsdl/schematron"?>
<!DOCTYPE TEI PUBLIC "-//TEI P5//DTD Main Document Type//EN" "http://www.tei-c.org/release/xml/tei/custom/schema/dtd/tei_all.dtd">
<TEI xmlns="http://www.tei-c.org/ns/1.0" xml:id="AntonioVallisneri.PrimiItinerisSpecimen">
    <teiHeader xml:lang="eng">
        <fileDesc>
            <titleStmt>
                <title></title>
            </titleStmt>
            <publicationStmt><p></p></publicationStmt>
            <sourceDesc><p></p></sourceDesc>
        </fileDesc>
    </teiHeader>
    <facsimile>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.r.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.r.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.V.r.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.V.r.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.v.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.v.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.r.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.r.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.v.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.v.eos-lat1.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.VII.r.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.VII.r.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.VII.v.eos-lat1.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.VII.v.eos-lat1"/>
        <graphic url="AntonioVallisneri.PrimiItinerisSpecimen.folio.IX.r_X.r.eos-lat1.020.jpg" xml:id="AntonioVallisneri.PrimiItinerisSpecimen.folio.IX.r_X.r.eos-lat1.020"/>
    </facsimile>
    <text>
        <body>
            <div type="edition" subtype="facsimile" n="urn:cts:italLit:AntonioVallisneri.PrimiItinerisSpecimen.eos-lat1" xml:lang="ita-Latn">
                <div type="textpart" subtype="folio" n="IV.r.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.r.eos-lat1">
                    <ab style="text-align: left" ana="4">Primi itineris per Montes Specimen<note type="appcrit" n="b">Montes <hi rend="italic">mutinenses</hi> Specimen</note> Physico-medicum.</ab>
                    <ab ana="5">Ab Antonio Vallisnerio de Nobilibus de Vallisneria in Patavino Archyliceo Publico<note type="appcrit" n="c">Archyliceo <hi rend="italic">Practicae Medicinae in primo loco</hi> Publico</note> Primario Theoricae Professore, ac <!-- <EOAindexperson main="Royal Society of London" elementorder="5" chapterorder="5"/> -->Regiae Societatis Angliae sodali, Sapientissimis, ac Praeclarissimis eiusdem Societatis Sodalibus dicatum:</ab>
                    <ab ana="6">ab Italo Idiomate in Latinum versum a L.v.eos-lat1.<note type="expl" n="2">These anonymous initials seem to indicate that the manuscript was translated into Latin from a previous Italian version, and not by Vallisneri himself. However, there are important hints that this may be a pretense. The handwriting in the main manuscript is unmistakably Vallisneri’s: since the document was draft (and a significantly reworked one, too), it is unlikely that he copied again the entire Latin text from another document, which in turn was a translation from an Italian text he had already edited. Furthermore, several studies prove that Vallisneri often used false names, or the names of his pupils, as a strategy to conceal and protect himself against potential criticisms—which in this case may have been addressed to the prose style of the document or to terminological misunderstandings. On this topic, see Generali 2004, 155–156, 176–177; 2007a, 383–412; Luzzini 2013a, 91; 2014a, 209. It is worth noting that the same initials (and, arguably, the same anonymous translator, whether real or not) appear—with an additional “S” in the end— in Vallisneri 1717c.</note><note type="appcrit" n="d">L.v.eos-lat1. <hi rend="italic">Scandianensi</hi></note></ab>
                    <ab style="text-align: left" ana="7">Sapientiss.mi, et Praeclariss.mi Sodales toto Terrarum Orbe celeberrimi.</ab>
                    <ab ana="8">Quis putasset, Sodales Amplissimi, vim ingeniorum, atque praestantiam studiis obesse, quis rationem, rem divinissimam, nos obtundere, ac pene ineptos efficere ad assequendam veritatem? Dictu id mirum, et monstro simile, sed eventu facillimum, mentis enim curiosa subtilitas adeo pulchras effingit, et parturit opiniones, concinne adeo, arguteque mentitur, ut plerique hominum fucatis orationibus capti, et tanquam laqueis irretiti erroribus pro sapientia utantur, iisque semel placitis indormire malint, quam liberari. Conatae sunt aevi nostri Academiae, inter quas vestra eminet, torporem hunc nobis excutere ad experimenta lacessendo; mihi quoque fas sit ante pedes vestros rudem</ab>
                </div>
                <div type="textpart" subtype="folio" n="IV.v.eos-lat1.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.IV.v.eos-lat1.eos-lat1">
                    <ab ana="8cont">libellum proicere<note type="appcrit" n="e">proi<hi rend="italic">j</hi>cere</note> non dissimilia tentantem, res quippe habet visu compertas, non ingenio. Horridulus quidem est atque incomptus, sed veniam dabitis inter Alpes nascenti. Per aestivas vacationes ea mihi vicinis montibus inerrandi cupido incessit; nec tela prae manibus ad figendas feras, sed calami, et pugillares gestabantur ad venandam veritatem. Praecipuam utilitatis discipulorum meorum rationem habui, arcanos latices, et inexploratas fontium medelas illis in reditu monstraturus.</ab>
                    <ab ana="9">Descendite paululum, viri gravissimi, de sapientia illa, qua <!-- <EOAindexperson main="Republic of Letters" elementorder="9" chapterorder="5"/> -->Literariae Reipublicae consulentes maria, terras, caelum respicitis. Praebete vos faciles exiguis conatibus meis, et pavidum adhuc ob magnitudinem beneficiorum vestrorum, nova quadam benignitatis culpa, in maiores ausus erigite.</ab>
                    <ab ana="10">Datam Patavii 1705</ab>
                    <ab style="text-align: right" ana="11">Addict.mus, et Obseq.mus famulus, et Sodalis</ab>
                    <ab style="text-align: right" ana="12">Antonius Vallisnerius</ab>
                </div>
                <div type="textpart" subtype="folio" n="V.r.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.v.eos-lat1.r.eos-lat1" xml:lang="ita-Latn">
                    <ab style="text-align: left" ana="13">All’<!-- <EOAindexperson main="Accademia dei Muti" elementorder="13" chapterorder="5"/> -->Accademia di Reggio. Etc.<note type="expl" n="3">Accademia dei Muti (“Academy of the Mute Ones”) of Reggio. Founded in 1673, it was mainly devoted to poetry and literature. It ceased to exist in 1751, after decades of senescence and—it seems—not particularly brilliant activity. On this topic, see Maylender 1929), 65–67. Vallisneri became a member of the Academy in 1711, after he was appointed the Chair of Theoretical Medicine at the University of Padua. See Porcia (di) 1733, LXXVII. See also the critical edition of this work: Porcia (di) 1986, 219–220, 220n</note></ab> 
                    <ab ana="14">Sprezzerete forse,<note type="appcrit" n="f">Sprezzerete <hi rend="italic">probabilmente</hi> forse</note> o riveritissimi Accademici,<note type="appcrit" n="g">o riveritissim<hi rend="italic">o amico</hi> Accademici</note> una filosofia, che si rampechi su per le balze più discoscese, e per inospiti monti cammini, e chiedendo risposte, dirò così, per imparare<note type="appcrit" n="h">cammini, e <hi rend="italic">che da quelli chieggia dirò così</hi> risposte <hi rend="italic">e notizie</hi> per <hi rend="italic">conoscere</hi> imparare<lb/>cammini, e <hi rend="italic">che da quelli chieggia dirà</hi> risposte<lb/>cammini, e chiedendo <hi rend="italic">colà</hi> risposte</note> il cupo genio della natura, e scoprir le sue leggi, da que’ taciti<note type="appcrit" n="i">leggi, <hi rend="italic">fra</hi> que<hi rend="italic">gli</hi> taciti</note> orrori; <!--mentre non pare-->, che<note type="appcrit" n="j">pare<hi rend="italic">ndo,</hi> che</note> abbian che fare né punto, né poco luoghi aspri, e deserti dalla<note type="appcrit" n="k">deserti <hi rend="italic">ed che paiono</hi> dalla</note> natura stessa abbandonati, col colto, e mite ingegno de’ filosofi, e segnatamente col vostro, dato solo alle muse più dilicate, ed agli studi più ameni. Scarseggiamo, potrete per avventura rimproverarmi, talmente delle ricchezze del vero, che dobbiamo partirsi da città fioritissime, dove si<note type="appcrit" n="l">dove <hi rend="italic">bollono cotanto</hi> si</note> coltivano con tanto ardore le belle arti, e le scienze, e portarsi, per acquistar la sapienza, dove appena poche orme di fiere ci guidano? Che cosa apportano alti scogli, acque<note type="appcrit" n="m">scogli, <hi rend="italic">e dirupi immensi, sassi</hi> acque</note> spezzate fra dirupi disaggradevoli, e terribili<note type="appcrit" n="n">e <hi rend="italic">sassi immensi</hi> terribili</note> caverne, se<note type="appcrit" n="o">caverne, <hi rend="italic">ne’ quali urtano, e si dirompono con istrepito per non dire con isdegno le acque cadenti, che</hi> se</note> non una spezie di confusione, e di oscurità agli occhi nostri, e timore e orrore alle menti? Così parmi di sentirvi parlare,<note type="appcrit" n="p">sentirvi <hi rend="italic">ridire</hi> parlare</note> né so, che ridire, se non che confido, che queste mie alpestri osservazioni portate avanti di voi perderanno molto della sua nativa rozzezza, mentre la verità, benché col testimonio de’ monti, e delle voraggini scoperta, e quando sarà addimesticata<note type="appcrit" n="q">scoperta, e <hi rend="italic">confermata confermata,</hi> quando sarà <hi rend="italic">e</hi> addimesticata</note> dalla gentile presenza di così nobile adunanza,<note type="appcrit" n="r">nobile <hi rend="italic">congresso</hi> adunanza</note> potrà facilmente cangiar aspetto, ed apparire più splendida,<note type="appcrit" n="s">più <hi rend="italic">speldente</hi> splendida</note> e decorosa, nella maniera appunto, che veggiamo le deformi nuvole, se toccano la vicinanza del sole, divenir belle, e dilettevoli.</ab>
                    <ab ana="15">A mezzo agosto presi il cammino verso i monti, non solo, per rilassare alquanto l’animo mio oppresso da più severi studi, ma ancora, ad esemplo degli oltramontani (che, per vero dire, indefessamente s’affaticano per illustrare la natura, e ci rimbrottano, e ci<note type="appcrit" n="t">illustrare <hi rend="italic">le loro patrie,</hi> e ci <hi rend="italic">rimproverano,</hi> e <hi rend="italic">murmurano</hi> ci<lb/>illustrare la natura. <hi rend="italic">Filosofica storia</hi> e ci</note> rinfacciano un ozio vile, e infindo)<note type="expl" n="4">Here, the author alludes to the French scholars. As a proud advocate of Italian science, language, and culture, Vallisneri was frequently involved in fierce debates with the “oltramontani” (literally, “those beyond the mountains”). On this topic, see Duchesneau 2009, CXII, CXXI, CXLV; Generali 1985; 2006; 2007a, 384–386; 2007b, 253–255; 2011b; Luzzini 2007, 74; 2013a, 217–226; Monti 2009, XLVIII, LII, LXVIII, LXXI, LXXVIII; Penso 1973, 194–201; Rappaport 1991 (now reprinted in 2011; 1997, 218–219. See also Vallisneri 1991, 519–520</note><note type="appcrit" n="u">e <hi rend="italic">infruttuoso</hi> infindo)</note> per rintracciare le nostre mediche, e naturali ricchezze, che senza invidia d’alcuno su quelli<note type="appcrit" n="v">su <hi rend="italic">ne’ monti</hi> quelli</note> abbondevolmente si trovano. Mi pare,<note type="appcrit" n="w">pare<hi rend="italic">va</hi></note> o Signori, anche una cosa, che non sia<note type="appcrit" n="x">non <hi rend="italic">fosse</hi> sia</note> priva del suo diletto, discendere<note type="appcrit" n="y">diletto, <hi rend="italic">come ora</hi> d<hi rend="italic">e</hi>scendere</note> ora in profonde valli, ora calcare le somme cime de’ monti, e porre il capo infin le nuvole, ora<note type="appcrit" n="z"><hi rend="italic">l</hi>ora</note> guardarsi all’intorno, e non vedere, che asprezza di terreno, e di cielo, dove attorniato da sole fiere, e da solo orrore vi si fomenta un non so che di grande, e degno di tante difficoltà, e dove allora un filosofo<note type="appcrit" n="aa">un &lt;<hi rend="italic">…</hi>&gt; filosofo</note> come maggior di se<note type="appcrit" n="ab"><hi rend="italic">m</hi>e</note> stesso, posto sopra i popoli, e sopra le torri </ab>
                </div>
                <div type="textpart" subtype="folio" n="V.v.eos-lat1.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.v.eos-lat1.v.eos-lat1" xml:lang="ita-Latn">
                    <ab style="text-align: left" ana="15cont">delle città, libero da ogni cura, e superiore ad ogni fortuna, senza lo strepito delle sonore scuole, tutto pien di natura tacito, e solo colla natura contrasta.<note type="appcrit" n="ac">natura <hi rend="italic">solamente</hi> contrasta</note></ab>
                </div>
                <div type="textpart" subtype="folio" n="VI.r.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.r.eos-lat1" xml:lang="ita-Latn">
                    <ab style="text-align: left" ana="16">La prima cosa, che mi venne fatto vedere<note type="appcrit" n="ad"><hi rend="bold">Margin note (left):</hi> S’aspetti d’essere a Scandiano etc.</note>fu la nobile<note type="appcrit" n="ae">la <hi rend="italic">g&lt;rande&gt; minera dello zolfo</hi> nobile</note> zolfatara lontana un miglio da Scandiano, posta<note type="appcrit" n="af">Scandiano <hi rend="italic">verso il monte,</hi> posta</note> alle radici del <hi rend="italic">Monte</hi> detto <hi rend="italic">del Gesso,</hi><note type="expl" n="5">Gypsum (CaSO<hi rend="subscript">4</hi>· 2H<hi rend="subscript">2</hi>O) is a mineral usually found in evaporitic deposits in association with sedimentary rocks. The gypsum layers of Mount Gesso are part of the gypsum-sulphur formation of the northern Apennines, whose thick evaporitic strata resulted from the Messinian salinity crisis which occurred in the late Miocene epoch (between 5.95 and 5.33 million years ago). During this epoch, a temporary closure of the Strait of Gibraltar made the Mediterranean Sea desiccate almost completely. This event originated the evaporitic rocks which are now visible along the northern borders of the Apennines, from Reggio Emilia to the Marche region. On this topic, see Bosellini 2005, 66–67; Luzzini 2011a, 105–107; 2011b; 2013a, 71–72; <!--<a href="http://www.vallisneri.it/affioramenti_gessosi.shtml">-->http://www.vallisneri.it/affioramenti_gessosi.shtml.</note> dietro<note type="appcrit" n="ag">Gesso, <hi rend="italic">sopra cui si veggono ancora le fondamenta d’un’antichissima ca fortezza, che</hi> dietro</note> un piccolo rivo<note type="appcrit" n="ah">piccolo <hi rend="italic">torrente</hi> rivo</note> che porta le acque nel<note type="appcrit" n="ai">acque <hi rend="italic">piovane di quel monte</hi> nel<hi rend="italic">l</hi>e</note> vicino Torrente Tresinara.<note type="expl" n="6">The Tresinaro River flows in the Province of Reggio Emilia. It is a tributary of the Secchia River. It originates in Felina (Castelnovo ne’ Monti, RE) and goes from southwest to northeast, eventually reaching Scandiano.</note> Questo fu, che<note type="appcrit" n="aj">fu <hi rend="italic">quello,</hi> che</note> scoprì la minera, mentre col radere ora da<note type="appcrit" n="ak">ora <hi rend="italic">la superficie,</hi> da</note> un canto, ora dall’altro, strascinava uniti co’ sassi, e terre, e arene, pezzi di puro zolfo, che osservati sino ne’ tempi antichi diedero occasione di ricercare il luogo, dove<note type="appcrit" n="al"><hi rend="bold">Margin note (right):</hi> Zolfat&lt;ara&gt;, fumo di zolfo</note> nasceva,<note type="appcrit" n="am">dove <hi rend="italic">onde</hi> nasceva</note> il quale, benché trovato, fu posto non so per quale scempiaggine<note type="appcrit" n="an">quale <hi rend="italic">balordagine</hi> scempiaggine</note> in una subita<note type="appcrit" n="ao">una <hi rend="italic">cieca</hi> subita</note> dimenticanza. Sotto il Serenissimo Principe <!--<EOAindexperson main="Luigi d’Este Juniore, Governor of Reggio and Marquess of Scandiano" elementorder="16" chapterorder="5"/>-->Luigi d’Este,<note type="expl" n="7">Luigi d’Este <hi rend="italic">Juniore</hi> (1648–1698), Governor of Reggio and Marquess of Scandiano. See Vallisneri 1991, 116</note> verso il fine del caduto secolo, seguitando il rivo<note type="appcrit" n="ap">il <hi rend="italic">torrente</hi> rivo</note> a portar tanto zolfo, quanto, accattandolo, bastava a povera<note type="appcrit" n="aq">a <hi rend="italic">certa</hi> povera</note> gente di<note type="appcrit" n="ar">gente <hi rend="italic">per accatto venderlo</hi> di</note> continuo lavorare zolfanelli da vendere, cadde in pensiero ad alcuni, di cercare<note type="appcrit" n="as">di<hi rend="italic">l d</hi>cercare</note> di nuovo questa minera, che facilmente fu ritrovata così<note type="appcrit" n="at">ritrovata <hi rend="italic">della quale era</hi> così</note> ferace, che da<note type="appcrit" n="au">che <hi rend="italic">basta per</hi> da</note> sé sola soddisfa, per ogni bisogno, a tutte le vicine città. Due<note type="appcrit" n="av">città. <hi rend="italic">Appena s’entra dentro la cava, che</hi> Due</note> sinora sono le cave fatte dall’arte, che comunicano insieme per<note type="appcrit" n="aw">insieme <hi rend="italic">nel fine</hi> per</note> lo giuoco necessario dell’aria, capaci<note type="appcrit" n="ax">dell’aria, <hi rend="italic">che vanno in</hi> capaci</note> di due uomini, che vi lavorino in piedi, e che co’ loro ordigni portino fuora la cavata minera.<note type="expl" n="8">The sulphur (S) veins in the gypsum-sulphur formation of the northern Apennines result from the biochemical activity of bacteria. Under anaerobic conditions, sulfate reducing bacteria produce hydrogen sulfide gas (H<hi rend="subscript">2</hi>S) from sulfate (SO<hi rend="subscript">4</hi>) in gypsum. H<hi rend="subscript">2</hi>S is then oxidized to elemental sulphur if exposed to oxygen. See Casati 1996, 518–519 Bosellini 2005, 66–67; Bosellini, Mutti, and Ricci Lucchi 1989, 133–169; Luzzini 2011b; 2011a, 106–107; 2013a, 72</note></ab>
                </div>
                <div type="textpart" subtype="folio" n="VI.v.eos-lat1.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.VI.v.eos-lat1.eos-lat1">                   
                </div>
                <div type="textpart" subtype="folio" n="VII.r.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.VII.r.eos-lat1">
                </div>
                <div type="textpart" subtype="folio" n="VII.v.eos-lat1.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.VII.v.eos-lat1.eos-lat1">                   
                </div>
                <div type="textpart" subtype="folio" n="IX.r_X.r.eos-lat1" facs="#AntonioVallisneri.PrimiItinerisSpecimen.folio.IX.r_X.r.eos-lat1.020">
                    <ab style="text-align: left" ana="21cont">veluti rami circumundique dispersi, cum<note type="appcrit" n="bw">dispersi, <hi rend="italic">ac veluti</hi> cum</note> pommis<note type="appcrit" n="bx">pomm&lt;<hi rend="italic">ae</hi>&gt;</note> sparsim infixis nutrimentum sugunt, ac maturescunt. Latitudo eiusdem ad pedes sex, longitudo ad<note type="appcrit" n="by">longitudo <hi rend="italic">usque</hi> ad</note> centum, usque adhuc exporrigitur. Inter saxa quaedam calcaria reconditur, quae aliquando a gypseis, tartareis,<note type="appcrit" n="bz">gypseis, <hi rend="italic">saxeis</hi> tartareis</note> terreisque stratis disterminatur. Differt<note type="appcrit" n="ca"><hi rend="bold">In the text:</hi> Difert</note> a Romana, uti referebant fossores, vulgo <hi rend="italic">canopi,</hi> quoniam ibi vena inter stratum, et stratum <hi rend="italic">orizontaliter</hi> explanatur, fodiuntque puteos, ut ipsam eruant, scandianensis vero oblique<note type="appcrit" n="cb">vero <hi rend="italic">fere transversaliter</hi> oblique</note> inter orizontalem, verticalemque occidentem versus sita<note type="appcrit" n="cc">versus <hi rend="italic">inclinata</hi> sita</note> sequitur stratorum, seu crustarum montis modo rectos, modo curvatos ordines. Hinc illa per puteos, haec per cuniculos facilius, minoribusque<note type="appcrit" n="cd">minori<hi rend="italic">s</hi>que</note> impensis eruitur.<note type="appcrit" n="ce">impensis <hi rend="italic">extrahitur</hi> eruitur</note> Nec adeo<note type="appcrit" n="cf">Nec <hi rend="italic">tam immensae</hi> adeo</note> vastae purissimi sulphuris glebae romanis in fodinis reperiuntur, sed improbo labore illud excavant impurius, quod<note type="appcrit" n="cg">impurius <hi rend="italic">immixtumque saxo quodam tophaceo</hi> quod</note> post ignem subviridi,<note type="appcrit" n="ch"><hi rend="bold">In the text:</hi> subviridique</note> ac diluta<note type="appcrit" n="ci">diluta<hi rend="italic">que</hi></note> flavedine perfusum expertum est.<note type="appcrit" n="cj">expertum <hi rend="italic">macrius pallidiusculum, macriusque appellatusque caballinum</hi> est</note> Nostrum vero<note type="appcrit" n="ck"><hi rend="bold">From this point on, text at p. 5 continues on an additional, unnumbered paper (IX). This is written only on the recto.</hi></note> ad<note type="appcrit" n="cl">vero <hi rend="italic">commune</hi> ad</note> <hi rend="italic">citrinum</hi> flavo<note type="appcrit" n="cm">citrinum <hi rend="italic">magis</hi> flavo</note> saturum vergit, et <hi rend="italic">virginale</hi> ad <hi rend="italic">croceum.</hi> Acidis scilicet particulis vitriolum<note type="expl" n="18">The term “vitriolum” (“vitriol”) refers to various kinds of metallic sulfates, including sulphuric acid (H<hi rend="subscript">2</hi>SO<hi rend="subscript">4</hi>).</note> redolentibus illud abundat, pingui magis istud, et inflammabili substantia. Hinc nostrum minorem olei sulphuris portionem per enchirisim<note type="expl" n="19">This is a latinization of the Ancient Greek word ἐγχείρησις (literally, “undertaking,” “operation,” or “task”).</note><note type="appcrit" n="cn">per <hi rend="italic">analysim</hi> enchirisim</note> donat. Ex quo sequitur, quod sulphurarii nostri morbis illis tentari non soleant, de quibus celeberrimus <!--<EOAindexperson main="Ramazzini, Bernardino" elementorder="21" chapterorder="5"/>-->Ramazzinus in egregio<note type="appcrit" n="co">in <hi rend="italic">sudato</hi> egregio</note> suo Opere de Morbis Artificum Cap. X scripsit.<note type="expl" n="20">Ramazzini 1700, Cap. X, De morbis quibus temari solent sulphurarii. Page references are to the second edition, Ramazzini 1703, 57–60. For a study of the bibliographical sources used by Ramazzini in this treatise, see Di Pietro 1981.</note> Omnes perpetuo sani degunt, non ultimum plebis operantis solatium. Cum etenim aura sulphuris acida sit ea, quae gladiolis hostilibus tenellas nostri corporis fibras pungit, et lacerat, ramosis,<note type="appcrit" n="cp"><hi rend="bold">From this point on, text continues on p. 5.</hi></note> ac plicatilibus copiosis involuta retunditur, viresque illae, quas in aliis exerit, edomantur. Hinc pro remediis pectori praecipue faventibus elaborandis Scandiani sulphur aptius aliis existimamus.</ab>
                </div>
            </div>
        </body>
    </text>
</TEI>

```


