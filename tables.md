## Tables

### Background

Tables represent tabular data. These do not sit well with XML, which has a tree structure, a fundamentally different data format. Nonetheless, Brill MRWs contain tables and they must be encoded in XML.

### Guidelines

See TEI Guidelines [Chapter 14.1 Tables](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/FT.html#FTTAB).

### Explanation

First off: Brill MRWs contain tabular data that needs to be represented as tables. Yet they also contain non-tabular data that is represented as tables. In particular, lists are sometimes encodes as tables, and tables as lists. Glosses – in the linguistic sense of linear glosses – are also encoded as tables. The reason is that for MRW staff,  XML is the only direct way to control the presentation of MRWs on the publication platforms. The other way – change requests – is slow and difficult to the point of impossible. The MRW CMSs and author tools like MS Word present a similar challenge: how to style the content? Tables have rows and columns and offer a solution for the presentation of glosses where alignment is of the highest importance. In this manual, the sections on lists and glosses deal with this matter in more detail.

In TEI, tables are encoded in a `<table>` element that contains `<row>` and `<cell>` elements. There is no `<column>` element! In XML, tables have no columns, only rows with cells in the same position (in a numerical sequence). A table may take a `<head>` element.

For the reason given above, MRW staff need to be able to set table and column width, and perform a number of other operations. Here is how. Table width and height are set with a `@style` attribute using CSS value pairs as values, e.g. "width:100%" or "height:50px". This can also be done with rows and cells. Column width can be set by setting the cell with in the first row. (In fact, the first _non-merged_ cell in the row, see below). It is then assumed that this setting applies to all cells below (the "column"). It is also assumed that if no width or other characteristic is applied, default settings apply.

Cells can be merged per row or column using the `@rows` and `@cols` attributes. `<cell rows="3">` for example indicates that this cell spans three rows.

Frames around tables are set in the following way: the `<table>` gets a `@style` attribute with the value "border-collapse: collapse; border: 1px solid black". (This is in fact a combination of multiple CSS value pairs). Additionally, a command must be given for every cell (and `<head>` element, if present): `@style="border: 1px solid black"`. Underlines and overlines for the top row (or any other row or column, for that matter) are set thus: give `<row>` a `@style` attribute with the value `style="border-bottom: 1 px solid"`.

Lastly the position of the contents in a cell on the vertical axis ("vertical alignment") can be set by `@style="vertical-align: top"`. The two other permissible values are "middle" and "bottom" .

### Example
```xml
<table cols="5">
    <head>1. The maximal syllable in Standard Chinese</head>
    <row>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
        <cell style="width: 60%">[kʰwai]</cell>
    </row>
    <row>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
        <cell>[kʰwai]</cell>
    </row>
</table>
```

### Recommendation

Use `@type` to indicate the type of cell contents, such as "data" or "head" .

