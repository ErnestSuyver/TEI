## Lists

### Background

Brill MRWs contain lists. These can be simple enumerations, or have a more complex structure. There is overlap with tables: a list can be thought of as a one-column table. Brill uses this rule of fist: a one-column table is better encoded as a list.

### Guidelines

See TEI Guidelines [Chapter 3.7 Lists](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html#COLI)

### Explanation

Lists in Brill MRWs contain items that may be labelled. A label might be an enumeration mark like a number, or text. TEI uses `<list>`, `<item>`, and `<label>` elements to encode this information. It is also possible to add a title, using the `<head>` element.

Brill content has four types of lists: with bulleted, numbered, lettered, and unmarked items. The `<label>` element is used to indicate the list type. It is placed before `<item>`. (In retrospect, a `@type` attribute might have been more useful…). If the label element is _empty and closed_, the list has _no enumeration marks_. If the label element is _absent_, the list is bulleted. If the label is _present and filled with letters_, the list is _lettered_. If the label is _present and filled with numbers_, the list is _numbered_.

### Example
```xml
<list>
    <item>Computer crimes--United Kingdom.</item>
    <item>Privacy, Right of--United Kingdom.</item>
    <item>Secrecy--Law and legislation--United Kingdom.</item>
    <item>Computer fraud--United Kingdom.</item>
</list>
```

