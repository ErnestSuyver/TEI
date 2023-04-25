## Letters

### Background

To date (May 2018), no editions of letters or correspondence can be counted among the Brill Reference Works, although some Brill monographs do contain this type of work. Also, the editions of the _Opera omnia_ by Gregory of Nyssa contains some works that may be considered letters. This section covers how to tag them.

### Guidelines

Letters are not a separate entity in TEI, like dictionaries or performance texts. Instead, most aspects relevant to letters are covered in [Chapter 4 Default Text Structure](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/DS.html). As always, TEI  offers a host of options. For reasons of simplicity and uniformity, Brill choses a minimum number of generic elements based on concrete needs.

### Explanation

Letters are works and can have different parts. The text itself may go into `<ab>` or `<p>`. It may be preceded by an `<opener>` containing a `<dateline>` and `<salute>`. The `<dateline>`, which often occurs in modern letters, may contain a `<placeName>` and `<date>`. The letter may be concluded with a `<closer>`, which may contain another `<salute>` and a `<signed>`. A postscriptum goes into a `<postscript>`. The whole work may go into a `<div type="letter">`.

Letters are texts and as such can have quotes, tables, images, or any other of the aspects covered elsewhere in these guidelines. As texts, letters can be published in editions. When this is the case, the letters will have numbered lines and these count as the parts of the logical structure, and not the `<opener>` or `<closer>` as such.

### Example
```xml
<div type="letter">
    <opener>
        <dateline>
            <placeName>Leiden</placeName>
            <date when="2018-05-23">May 23, 2018</date>
        </dateline>
        <salute>Dear <persName ref="some URI">Reader</persName>,</salute>
            </opener>
                <p>This is a letter to you, which we hope will be of some benefit should you be in search of a sample letter encoded in the TEI. We have based this letter on the <orgName ref="#org\_teic">Text Encoding Initiative Consortium</orgName> Guidelines. The Guidelines can be found <ref target="http://www.tei-c.org/Guidelines/">here</ref>.
                </p>
            </opener>
            <closer>
                <salute>Sincerely,</salute>
                <signed><orgName ref="#Brill">Brill Academic Publishers</orgName></signed>
            </closer>
            <postscript>
                <label>P.S.</label>
                <p>Be sure to check out the Brill TEI Guidelines: <ref target="http://gitli.gitlab.io/book-header/">"Letters"</ref> for an extended discussion of letters as an encoded document genre.</p>
            </postscript>
        </div>
```

### See also

* correspSearch: [https://correspsearch.net/](https://correspsearch.net/)
* Letters of Vincent van Gogh: [http://vangoghletters.org/vg/letters.html](http://vangoghletters.org/vg/letters.html)
* Letters of 1916: [http://letters1916.maynoothuniversity.ie/explore/browse/all](http://letters1916.maynoothuniversity.ie/explore/browse/all)
* TEI SIG for correspondence: [https://wiki.tei-c.org/index.php/SIG:Correspondence](https://wiki.tei-c.org/index.php/SIG:Correspondence)
* Useful template for a letter in TEI: [https://gist.github.com/dhscratch/378e31e8e69dbb54d82b6be2634f4e7f](https://gist.github.com/dhscratch/378e31e8e69dbb54d82b6be2634f4e7f)
* Journal article: Peter Stadler, Marcel Illetschko, and Sabine Seifert, "Towards a Model for Encoding Correspondence in the TEI: Developing and Implementing `<correspDesc>`", _Journal of the Text Encoding Initiative_ Issue 9 | September 2016 - December 2017 : Selected Papers from the 2014 TEI Conference; URL: [https://journals.openedition.org/jtei/1433](https://journals.openedition.org/jtei/1433)

