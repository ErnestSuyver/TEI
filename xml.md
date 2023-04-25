## XML

### intro

XML stands for _Extensible Markup Language_. The idea is to "separate concerns", i.e separate the presentation of a text from its structure. So if a text has an author, a title and a body, these three things would be tagged as such. And if the text were printed, or published as an ebook, a stylesheet would determine how that title would look on paper or on the screen.

### tags

The XML tags surround the content they tag. So there is always an opening and a closing tag:

```xml
<author>Kate</author>
<title>Peanut butter</title>
<body>Peanut butter is nice and healthy.</body>
```

There is _one_ exception: when a tag has no concents, the opening and closing tag may be combined: `<author/>`. 


### elements and attributes

`<author>` is an element. It can have an attribute, for example `<author dateofbirth="20020202">`. In this case `dateofbirth` is an attribute, and `20020202` is its value.

### well-formed

An XML file has an `.xml` extension and always starts with the XML declaration to tell the computer it is XML: `<?xml version="1.0" encoding="UTF-8"?>`

A tag _always_ has pointy brackets and there must _always_ be an opening and end tag. 

Also, tags may be nested - sit inside each other, like `<author><firstname>Kate</firstname></author>` but can _never_ overlap (like `<author><firstname>Kate</author></firstname>`)

If any of these things is wrong, the XML file is not "well-formed" and your computer will be unhappy. 

### valid

Tags can be anything you want. In any language, in any script. This also means that _nobody knows what they mean - except you_. Even for a seemingly obvious tag like `<author>`, you don't know how it is used unless someone tells you. You can write down how you use the tags. This is called a _schema_. A schema tells the computer what tags you use, and how they may be combined.

For example, you may say: in my world, the author tag always has two children, first name and last name. They may not be empty, and there must always be the two of them. 

Some XML files contain a pointer to the schema, so the computer understands what the rules are. That may look something like this `<!DOCTYPE encyclopedia SYSTEM "Encyclopedia.dtd">`.

If your XML file conforms to these rules, it is _valid_. If not, your computer will be unhappy. 

At Brill, the _BrillOnline Reference Works_ "platform" expects XML files to be one of two schemas:

1. [encyclopedia](enc.md)
2. [Brill TEI EPidoc](brill_tei_epidoc.md)

### Learn more

Make sure to follow the [XML Tutorial](https://www.w3schools.com/xml/default.asp) at W3 Schools. It is short, clear, and you can tinker online without breaking anything.

### XML editor

XML is plain text and so any text editor may be used to create or edit XML files. Many have plugins that allow you to style your XML and to validate it.

There also exist dedicated XML editors (sometimes called "parsers"). Scholars tend to use _Oxygen_, which is very powerful but costly. Numerous open and free alternatives exist. 

At Brill, we have a limited number of licences for _Oxygen-. In the remote, we have _XML Copy Editor_ that anyone can use.
