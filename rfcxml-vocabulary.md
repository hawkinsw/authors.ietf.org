---
title: RFCXML Vocabulary
description: 
published: true
date: 2021-11-03T09:25:33.811Z
tags: 
editor: markdown
dateCreated: 2021-11-02T22:58:38.001Z
---


## abstract
## Tabs {.tabset}
### Usage
Contains the Abstract of the document. See RFC7322 for more information on restrictions for the Abstract.

Can be child of: [`front`](/rfcxml-elements#front)
Contents: ([`dl`](/rfcxml-elements#dl), [`ol`](rfcxml-elements#ol), [`t`](rfcxml-elements#t), [`ul`](rfcxml-elements#ul))+
### Attributes
#### "anchor"
Document-wide unique identifier for this element.
### Schema
```
   abstract =
     element abstract {
       attribute xml:base { text }?,
       attribute xml:lang { text }?,
       attribute anchor { xsd:ID }?,
       attribute pn { text }?,
       (dl | ol | t | ul)+
     }
```

## address
## Tabs {.tabset}
### Usage
Provides address information for the author.

Can be child of: [`author`](rfcxml#author), [`contact`](/rfcxml-elements#contact)
Contents: [`postal?`](rfcxml-elements#postal),[`phone?`](rfcxml-elements#phone),[`email*`](rfcxml-elements#email),[`uri?`](rfcxml-elements#uri)

## annotation
## Tabs {.tabset}
### Usage
Provides additional prose augmenting a bibliographic reference. This text is intended to be shown after the rest of the generated reference text.

Can be child of: [`reference`](/rfcxml-elements#reference)
Contents: ( text | [`bcp14`](rfcxml-elements#bcp14) | [`cref`](rfcxml-elements#cref) | [`em`](rfcxml-elements#em) | [`eref`](rfcxml-elements#eref) | [`iref`](rfcxml-elements#iref) | [`strong`](rfcxml-elements#strong) | [`sub`](rfcxml-elements#sub) | [`sup`](rfcxml-elements#sup) | [`tt`](rfcxml-elements#tt) | [`u`](rfcxml-elements#u) | [`xref`](rfcxml-elements#xref) )*

## area
## Tabs {.tabset}
### Usage
Provides information about the IETF area to which this document relates (currently not used when generating documents).

The value ought to be either the full name or the abbreviation of one of the IETF areas as listed on http://www.ietf.org/iesg/area.html. A list of full names and abbreviations will be kept by the RFC Series Editor.

Can be child of: [`front`](/rfcxml-elements#front)
Contents: text

## artset
## Tabs {.tabset}
### Usage
This element allows for the support of multiple artwork formats, in order to provide suitable artwork for different output formats.

When multiple [`artwork`](/rfcxml-elements#artwork) instances are provided within one `artset` element, the renderer will try to pick the [`artwork`](/rfcxml-elements#artwork) instance which is most appropriate for its current output format from the given alternatives.

If more than one [`artwork`](/rfcxml-elements#artwork) element with the same "type" is found within an [`artset`](/rfcxml-elements#artset) element, the renderer could select the first one, or possibly choose between the alternative instances based on the output format and some quality of the alternatives that make one more suitable than the others for that particular format, such as size, aspect ratio, etc.

Can be child of: [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`figure`](/rfcxml-elements#figure), [`li`](/rfcxml-elements#li), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th)
Contents: `artwork+`
### Attributes
#### "anchor"
Document-wide unique identifier for this element.

## artwork
## Tabs {.tabset}
### Usage
This element allows the inclusion of "artwork" in the document. [`artwork`](rfcxml-elements#artwork) provides full control of horizontal whitespace and line breaks; thus, it is used for a variety of things, such as diagrams ("line art") and protocol unit diagrams. Tab characters (U+0009) inside of this element are prohibited.

Alternatively, the "src" attribute allows referencing an external graphics file, such as a vector drawing in SVG or a bitmap graphic file, using a URI. In this case, the textual content acts as a fallback for output representations that do not support graphics; thus, it ought to contain either (1) a "line art" variant of the graphics or (2) prose that describes the included image in sufficient detail.

In order to include alternative artwork expressions for different output formats, you should provide multiple [`artwork`](rfcxml-elements#artwork) elements enclosed within an [`artset`](rfcxml-elements#artset). The text renderer will prefer instances with type="ascii-art", while the HTML and PDF renderers will prefer instances with type="svg".

In previous versions of the schema, the [`artwork`](rfcxml-elements#artwork) element was also used for source code and formal languages; this is now done with [`sourcecode`](rfcxml-elements#sourcecode).

There are at least five ways to include SVG in artwork in Internet- Drafts:

* Inline, by including all of the SVG in the content of the element, such as:
```xml
<artwork type="svg"><svg xmlns="http://www.w3.org/2000/ svg...">
```
* Inline, but using XInclude (see Appendix B.1), such as:
```xml
<artwork type="svg"><xi:include href=...>
```
* As a data: URI, such as:
```xml 
<artwork type="svg" src="data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww...">
```
* As a URI to an external entity, such as:
```xml
<artwork type="svg" src="http://www.example.com/...">
```
* As a local file, such as:
```xml
<artwork type="svg" src="diagram12.svg">
```

The use of SVG in Internet-Drafts and RFCs is covered in much more detail in [RFC7996].

The above methods for inclusion of SVG art can also be used for including text artwork, but using a data: URI is probably confusing for text artwork.

Formatters that do pagination should attempt to keep artwork on a single page. This is to prevent artwork that is split across pages from looking like two separate pieces of artwork.

See Section 5 for a description of how to deal with issues of using "&" and "<" characters in artwork.

Can be child of: [`artset`](/rfcxml-elements#artset), [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`figure`](/rfcxml-elements#figure), [`li`](/rfcxml-elements#li), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th)
Contents: ( [`text*`](rfcxml-elements#text) | [`svg`](rfcxml-elements#svg) )

### Attributes
#### "align"
Controls whether the artwork appears left justified, centered, or right justified.

Possible values: `( "left" | "center" | "right" )`
Default value: `"left"`

#### "alt"
Alternative text description of the artwork (which is more than just a summary or caption). When the art comes from the "src" attribute and the format of that artwork supports alternate text, the alternative text comes from the text of the artwork itself, not from this attribute. The contents of this attribute are important to readers who are visually impaired, as well as those reading on devices that cannot show the artwork well, or at all.

#### "anchor"
Document-wide unique identifier for this element.

#### "height"
TBD

#### "name"
A filename suitable for the contents (such as for extraction to a local file). This attribute can be helpful for other kinds of tools (such as automated syntax checkers, which work by extracting the artwork). Note that the "name" attribute does not need to be unique for [`artwork`](rfcxml-elements#artwork) elements in a document. If multiple [`artwork`](rfcxml-elements#artwork) elements have the same "name" attribute, a processing tool might assume that the elements are all fragments of a single file, and the tool can collect those fragments for later processing.

#### "src"
The URI reference of a graphics file RFC3986, or the name of a file on the local disk. This can be a "data" URI RFC2397 that contains the contents of the graphics file. Note that the inclusion of art with the "src" attribute depends on the capabilities of the processing tool reading the XML document. Tools need to be able to handle the file: URI, and they should be able to handle http: and https: URIs as well. The prep tool will be able to handle reading the "src" attribute.

If no URI scheme is given in the attribute, the attribute is considered to be a local filename relative to the current directory. Processing tools must be careful to not accept dangerous values for the filename, particularly those that contain absolute references outside the current directory. Document creators should think hard before using relative URIs due to possible later problems if files move around on the disk. Also, documents should most likely use explicit URI schemes wherever possible.

In some cases, the prep tool may remove the "src" attribute after processing its value. See RFC7998 for a description of this.

#### "type"
Specifies the format of the artwork. The value of this attribute is free text with certain values designated as preferred.

The preferred values for [`artwork`](/rfcxml-elements#artwork) types are:

* ascii-art
* binary-art
* svg

Values that don't describe the format, such as "call-flow" or "hex-dump" were mentioned in RFC7991, but are not supported here; they are instead candidates for use with another future attribute to describe the artwork content.

A complete list of the preferred values is maintained on the RFC Editor web site, and that list is expected to be updated over time. Thus, a consumer of this attribute should not cause a failure when it encounters an unexpected type or no type is specified. The table will also indicate which type of art can appear in plain-text output (for example, type="svg" cannot).

#### "width"
TBD

## aside
## Tabs {.tabset}
### Usage
This element is a container for content that is semantically less important or tangential to the content that surrounds it.
 
Can be child of: [`dd`](/rfcxml-elements#dd), [`section`](/rfcxml-elements#section)
Contents: ( [`artset`](rfcxml-elements#artset) | [`artwork`](rfcxml-elements#artwork) | [`blockquote`](rfcxml-elements#blockquote) | [`dl`](rfcxml-elements#dl) | [`figure`](rfcxml-elements#figure) | [`iref`](rfcxml-elements#iref) | [`ol`](rfcxml-elements#ol) | [`t`](rfcxml-elements#t) | [`table`](rfcxml-elements#table) | [`ul`](rfcxml-elements#ul) )*
### Attributes
#### "anchor"
Document-wide unique identifier for this element.

## author
## Tabs {.tabset}
### Usage
Provides information about a document's author. This is used both for the document itself (at the beginning of the document) and for referenced documents.

The [`author`](rfcxml-elements#author) elements contained within the document's [`front`](rfcxml-elements#front) element are used to fill the boilerplate and also to generate the "Author's Address" section (see RFC7322).

Note that an "author" can also be just an organization (by not specifying any of the "name" attributes, but adding the [`organization`](rfcxml-elements#organization) child element).

Furthermore, the "role" attribute can be used to mark an author as "editor". This is reflected both on the front page and in the "Author's Address" section, as well as in bibliographic references. Note that this specification does not define a precise meaning for the term "editor".

Can be child of: [`front`](/rfcxml-elements#front), [`section`](/rfcxml-elements#section)
Contents: organization?, address?

### Attributes
#### "anchor"
Document-wide unique identifier for this element.

#### "asciiFullname" 
The Latin script equivalent of the author's full name.

#### "asciiInitials" 
The Latin script equivalent of the author's initials, to be used in conjunction with the separately specified asciiSurname.

#### "asciiSurname" 
The Latin script equivalent of the author's surname, to be used in conjunction with the separately specified asciiInitials.

#### "fullname" 
The full name (used in the automatically generated "Author's Address" section). Although this attribute is optional, if one or more of the "asciiFullname", "asciiInitials", or "asciiSurname" attributes does not have values, the "fullname" attribute is required.

#### "initials" 
An abbreviated variant of the given name(s), to be used in conjunction with the separately specified surname. It usually appears on the front page, in footers, and in references.

Some processors will post-process the value -- for instance, when it only contains a single letter (in which case they might add a trailing dot). Relying on this kind of post-processing can lead to results varying across formatters and thus ought to be avoided.

#### "role" 
Specifies the role the author had in creating the document.

#### "surname" 
The author's surname, to be used in conjunction with the separately specified initials. It usually appears on the front page, in footers, and in references.

## back
## Tabs {.tabset}
### Usage
Contains the "back" part of the document: the references and appendices. In [`back`](rfcxml-elements#back), [`section`](rfcxml-elements#section) elements indicate appendices.

Can be child of: [`rfc`](/rfcxml-elements#rfc)
Contents: `displayreference*, references*, section*`

## bcp14
## Tabs {.tabset}
### Usage
Marks text that are phrases defined in BCP14 such as "MUST", "SHOULD NOT", and so on. When shown in some of the output representations, the text in this element might be highlighted. The use of this element is optional.

This element is only to be used around the actual phrase from BCP 14, not the full definition of a requirement. For example, it is correct to say "The packet \<bcp14>MUST\</bcp14> be dropped.", but it is not correct to say "\<bcp14>The packet MUST be dropped.\</bcp14>".

Can be child of: [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`refcontent`](/rfcxml-elements#refcontent), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt).
Contents: `text`

## blockquote
## Tabs {.tabset}
### Usage
Specifies that a block of text is a quotation.

Can be child of: [`aside`](/rfcxml-elements#aside), [`li`](/rfcxml-elements#li), [`section`](/rfcxml-elements#section)
Contents: ( ( artset | artwork | dl | figure | ol | sourcecode | t | ul )+ | ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | tt | u | xref )+ )

### Attributes
#### anchor
Document-wide unique identifier for this element.

#### cite
The source of the citation. This must be a URI. If the "quotedFrom" attribute is given, this URI will be used by processing tools as the link for the text of that attribute.

#### quotedFrom
Name of person or document the text in this element is quoted from. A formatter should render this as visible text at the end of the quotation.

## boilerplate
## Tabs {.tabset}
### Usage
Holds the boilerplate text for the document. This element is filled in by the prep tool.

This element contains [`section`](/rfcxml-elements#section) elements. Every [`section`](/rfcxml-elements#section) element in this element must have the "numbered" attribute set to "false".

Can be child of: [`front`](/rfcxml-elements#front)
Contents: section+

## br
## Tabs {.tabset}
### Usage
Inserts a forced break. Use sparingly. In most situations, it's better to insert U+200B, ZERO WIDTH SPACE, in order to encourage line breaking at a point where it would otherwise not occur.

Can be child of: [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`strong`](/rfcxml-elements#strong), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`title`](/rfcxml-elements#title), [`tt`](/rfcxml-elements#tt)
Contents: empty

## city
## Tabs {.tabset}
### Usage
Gives the city name in a postal address.

Can be child of: [`postal`](/rfcxml-elements#postal)
Contents: text

### Attributes
#### "ascii"

The ASCII equivalent of the [`city`](/rfcxml-elements#city) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## cityarea
## Tabs {.tabset}
### Usage
Where postal addresses use city subdivisions, these are mapped to the [`cityarea`](/rfcxml-elements#cityarea) element. Korean addresses would use this for a city district, for instance. Countries known to use this element are Ascension Island, China, Iran, South Korea, and Thailand.

Can be child of: [`postal`](/rfcxml-elements#postal)
Content schema: text

### Attributes
#### ascii 
The ASCII equivalent of the [`cityarea`](rfcxml-elements#cityarea) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## code
## Tabs {.tabset}
### Usage
Gives the postal region code.

This element can be a child element of [`postal`](/rfcxml-elements#postal).
Contents: text

### Attributes
#### "ascii" 
The ASCII equivalent of the [`code`](/rfcxml-elements#code) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## contact
## Tabs {.tabset}
### Usage
Provides information about contributors. This element can be used inline within a [`t`](/rfcxml-elements#t), and will be rendered with name only, similarly to how [`author`](/rfcxml-elements#author) is rendered in a [`reference`](/rfcxml-elements#reference), or it can be used as a direct child of [`section`](/rfcxml-elements#section), where it will be rendered the same way as an author address block within the "Authors' Addresses" section.

Note that a "contact" can also be just an organization (by not specifying any of the "name" attributes, but adding the `organization` child element).

This element can be a child element of [`section`](/rfcxml-elements#section), [`t`](/rfcxml-elements#t)
Contents: organization?, address?

### Attributes
#### anchor
Document-wide unique identifier for this element.

#### asciiFullname
The Latin script equivalent of the contact's full name.

#### asciiInitials
The Latin script equivalent of the contact's initials, to be used in conjunction with the separately specified asciiSurname.

#### asciiSurname
The Latin script equivalent of the contact's surname, to be used in conjunction with the separately specified asciiInitials.

#### fullname
The full name. Although this attribute is optional, if one or more of the "asciiFullname", "asciiInitials", or "asciiSurname" attributes does not have values, the "fullname" attribute is required.

#### initials
An abbreviated variant of the given name(s), to be used in conjunction with the separately specified surname.

#### surname
The contact's surname, to be used in conjunction with the separately specified initials.

## country
## Tabs {.tabset}
### Usage
Specifies the country name in a postal address. All common and official country names should be recognized; in addition two- and three-letter country codes according to ISO 3166 are recognized.

xml2rfc has a help option which will list all names and country codes it recognizes as valid country names: xml2rfc --country-help .

This element can be a child element of [`postal`](/rfcxml-elements#postal).
Contents: [`text`](/rfcxml-elements#text)

### Attributes
#### ascii
The ASCII equivalent of the [`country`](/rfcxml-elements#country) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## cref
## Tabs {.tabset}
### Usage
Represents a comment.

Comments can be used in a document while it is work in progress. They might appear either inline and visually highlighted, at the end of the document, or not at all, depending on the formatting tool.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt)
Content schema: ( text | br | em | eref | strong | sub | sup | tt | xref )*

### Attributes
#### anchor
Document-wide unique identifier for this element.

#### display
Suggests whether or not the comment should be displayed by formatting tools. This might be set to "false" if you want to keep a comment in a document after the contents of the comment have already been dealt with.
  
Possible values: ( "true" | "false" )
Default value: "true"

#### source 
Holds the "source" of a comment, such as the name or the initials of the person who made the comment.

## date
## Tabs {.tabset}
### Usage
Provides information about the publication date. This element is used for two cases: the boilerplate of the document being produced, and inside bibliographic references that use the [`front`](rfcxml-elements#front) element.

Bibliographic references:
* In order to be able to specify fuzzy dates, such as "2002-2003", "Second quarter 2010", etc., the date element is now permitted to have text content in addition to the "year", "month", and "day" attributes. If there is only text content, it will be rendered as is. If there is both text content and date components, both will be rendered, with the expanded date components in parentheses.

Boilerplate for Internet-Drafts and RFCs:
* This element defines the date of publication for the current document (Internet-Draft or RFC). When producing Internet-Drafts, the prep tool uses this date to compute the expiration date (see [IDGUIDE]). When one or more of "year", "month", or "day" are left out, the prep tool will attempt to use the current system date if the attributes that are present are consistent with that date.

In dates in [`rfc`](rfcxml-elements#rfc) elements, the month must be a number or a month in English. The prep tool will silently change text month names to numbers. Similarly, the year must be a four-digit number.

When the prep tool is used to create Internet-Drafts, it will warn if the draft has a [`date`](rfcxml-elements#date) element in the boilerplate for itself that is more than 3 days away from today. To avoid this problem, authors might simply not include a `date` element in the boilerplate.

This element can be a child element of [`front`](/rfcxml-elements#front)
Content schema: text

### Attributes
#### day 
The day of publication.

#### month
The month of publication.

#### year 
The year of publication.

## dd
## Tabs {.tabset}
### Usage
The definition part of an entry in a definition list.

This element can be a child element of [`dl`](/rfcxml-elements#dl).
Content schema: ( ( artset | artwork | aside | dl | figure | ol | sourcecode | t | table | ul )+ | ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | tt | u | xref )+ )

### Attributes
#### anchor
Document-wide unique identifier for this element.

## displayreference
## Tabs {.tabset}
### Usage
This element gives a mapping between the anchor of a reference and a name that will be displayed instead. This allows authors to display more mnemonic anchor names for automatically included references. The mapping in this element only applies to `xref` elements whose format is "default". For example, if the reference uses the anchor "RFC6949", the following would cause that anchor in the body of displayed documents to be "RFC-dev":
```xml
<displayreference target="RFC6949" to="RFC-dev"/>
```
If a reference section is sorted, this element changes the sort order.

This element can be a child element of [`back`](/rfcxml-elements#back).

### Attributes
#### target (Required)
This attribute must be the name of an anchor in a [`reference`](/rfcxml-elements#reference) or [`referencegroup`](/rfcxml-elements#referencegroup) element.

#### to (Required)
This attribute is a name that will be displayed as the anchor instead of the anchor that is given in the [`reference`](rfcxml-elements#reference) element. The string given must start with one of the following characters: 0-9, a-z, or A-Z. The other characters in the string must be 0-9, a-z, A-Z, "-", ".", or "_".

## dl
## Tabs {.tabset}
### Usage
A definition list. Each entry has a pair of elements: a term ([`dt`](rfcxml-elements#dt)) and a definition ([`dd`](rfcxml-elements#dd)). (This is slightly different and simpler than the model used in HTML, which allows for multiple terms for a single definition.)

This element can be a child element of [`abstract`](/rfcxml-elements#abstract), [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), [`note`](/rfcxml-elements#note), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th).
Content schema: ( [`dt`](/rfcxml-elements#dt), [`dd`](/rfcxml-elements#dd) )+

### Attributes
#### anchor
Document-wide unique identifier for this element.

#### indent
Indicates the indentation to be used for the rendering of the second and following lines of the item (the first line starts with the term, and is not indented). The indentation amount is interpreted as characters when rendering plain-text documents, and en-space units when rendering in formats that have richer typographic support such as HTML or PDF. One en-space is assumed to be the length of 0.5 em-space in CSS units.

Default value: "3"

#### newline
The "newline" attribute defines whether or not the term appears on the same line as the definition. newline="false" indicates that the term is to the left of the definition, while newline="true" indicates that the term will be on a separate line.

Possible values: ( "true" | "false" )
Default value: "false"

#### spacing
Defines whether or not there is a blank line between entries. spacing="normal" indicates a single blank line, while spacing="compact" indicates no blank line between entries.

Possible values: ( "normal" | "compact" )
Default value: "normal"

## dt
## Tabs {.tabset}
### Usage
The term being defined in a definition list.

This element can be a child element of [`dl`](rfcxml-elements#dl).
Content schema: ( text | [bcp14](/rfcxml-elements#bcp14) | [br](/rfcxml-elements#br) | [cref](/rfcxml-elements#cref) | [em](/rfcxml-elements#em) | [eref](/rfcxml-elements#eref) | [iref](/rfcxml-elements#iref) | [strong](/rfcxml-elements#strong) | [sub](/rfcxml-elements#sub) | [sup](/rfcxml-elements#sup) | [tt](/rfcxml-elements#tt) | [xref](/rfcxml-elements#xref) )*
### Attributes
#### anchor 
Document-wide unique identifier for this element.

## em
## Tabs {.tabset}
### Usage
Indicates text that is semantically emphasized. In HTML and PDF rendering, text enclosed within this element will be displayed as italic after processing; in text rendering it will be preceded and folled by an underline character. This element can be combined with other character formatting elements, and the formatting will be additive.

This element can be a child element of [`annotation`](rfcxml-elements#annotation), [`blockquote`](rfcxml-elements#blockquote), [`cref`](rfcxml-elements#cref), [`dd`](rfcxml-elements#dd), [`dt`](rfcxml-elements#dt), [`li`](rfcxml-elements#li), [`name`](rfcxml-elements#name), [`refcontent`](rfcxml-elements#refcontent), [`strong`](rfcxml-elements#strong), [`sub`](rfcxml-elements#sub), [`sup`](rfcxml-elements#sup), [`t`](rfcxml-elements#t), [`td`](rfcxml-elements#td), [`th`](rfcxml-elements#th), [`tt`](rfcxml-elements#tt),[`xref`](rfcxml-elements#xref).
Content schema: ( text | [bcp14](/rfcxml-elements#bcp14) | [br](/rfcxml-elements#br) | [cref](/rfcxml-elements#cref) | [eref](/rfcxml-elements#eref) | [iref](/rfcxml-elements#iref) | [strong](/rfcxml-elements#strong) | [sub](/rfcxml-elements#sub) | [sup](/rfcxml-elements#sup) | [tt](/rfcxml-elements#tt) | [xref](/rfcxml-elements#xref) )*

## email
## Tabs {.tabset}
### Usage
Provides an email address.

The value is expected to be the addr-spec defined in Section 2 of RFC6068.

Multiple email addresses are permitted.

This element can be a child element of [`address`](/rfcxml-elements#address).

Content schema: text
#### ascii

The ASCII equivalent of the author's email address. This is only used if the email address has any internationalized components.

## eref
## Tabs {.tabset}
### Usage
Represents an "external" link (as specified in the "target" attribute). This is useful for embedding URIs in the body of a document.

If the [`eref`](/rfcxml-elements#eref) element has non-empty text content, the content is used as the displayed text that is linked. Otherwise, the value of the "target" attribute is used as the displayed text.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt), .

Content schema: text
### Attributes
#### brackets

Determines the type of brackets that an eref will be rendered with. "angle" will render with angle brackets, and "none" will render with no brackets in HTML and PDF, and with parentheses by the text renderer.

Possible values: ( "none" | "angle" )
Default value: "none"

#### target (Required)

URI of the link target (RFC3986). This must begin with a scheme name (such as "https://") and thus not be relative to the URL of the current document.

## extaddr
## Tabs {.tabset}
### Usage
Extra address information. This element can be used for address parts more specific than a street, for instance apartment numbers, suite numbers, building parts, etc.

This element can be a child element of [`postal`](/rfcxml-elements#postal).

Content schema: text
### Attributes
#### ascii

The ASCII equivalent of the [`extaddr`](/rfcxml-elements#extaddr) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## figure
## Tabs {.tabset}
### Usage
Contains a figure with a caption with the figure number. If the element contains a [`name`](/rfcxml-elements#name) element, the caption will also show that name.

This element can be a child element of [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), and [`th`](/rfcxml-elements#th).

Content schema: name?, iref*, ( artset | artwork | sourcecode )+
### Attributes
#### align

Possible values: ( "left" | "center" | "right" )
Default value: "left"
#### alt
TBD

#### anchor
Document-wide unique identifier for this element.

#### height
TBD

#### src
TBD

#### suppress-title
Possible values: ( "true" | "false" )
Default value: "false"

#### title
Deprecated. Use the [`name`](/rfcxml-elements#name) element instead.

#### width
TBD

## front
## Tabs {.tabset}
### Usage
Represents the "front matter" metadata (such as author information), the Abstract, and additional notes.

A [`front`](/rfcxml-elements#front) element may have more than one [`seriesInfo`](/rfcxml-elements#seriesInfo) element. Each should contain a "name" attribute with the series name and a "value" attribute with the series number; other uses of [`front`](/rfcxml-elements#front)[`seriesInfo`](/rfcxml-elements#seriesInfo) described in [RFC7991] are deprecated.

This element can be a child element of [`reference`](/rfcxml-elements#reference) and [`rfc`](/rfcxml-elements#rfc).

Content schema: title, seriesInfo\*, author+, date?, area\*, workgroup\*, keyword\*, abstract?, note\*, boilerplate?, toc?

## iref
## Tabs {.tabset}
### Usage
Provides terms for the document's index.

Index entries can be either regular entries (when just the "item" attribute is given) or nested entries (by specifying "subitem" as well), grouped under a regular entry.

Index entries generally refer to the exact place where the [`iref`](/rfcxml-elements#iref) element occurred. An exception is the occurrence as a child element of [`section`](/rfcxml-elements#section), in which case the whole section is considered to be relevant for that index entry. In some formats, index entries of this type might be displayed as ranges.

When the prep tool is creating index content, it collects the items in a case-sensitive fashion for both the item and subitem level.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`figure`](/rfcxml-elements#figure), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`section`](/rfcxml-elements#section), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`table`](/rfcxml-elements#table), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt), .

Content schema: empty

### Attributes
#### item (Required)
The item to include.

#### primary
Setting this to "true" declares the occurrence as "primary", which might cause it to be highlighted in the index. There is no restriction on the number of occurrences that can be "primary".

Possible values: ( "true" | "false" )
Default value: "false"

#### subitem
The subitem to include.

## keyword
## Tabs {.tabset}
### Usage
Specifies a keyword applicable to the document.

Note that each element should only contain a single keyword; for multiple keywords, the element can simply be repeated.

Keywords are used both in the RFC Index and in the metadata of generated document representations. They are not reflected in the HTML, PDF, or text rendering of the document.

This element can be a child element of [`front`](/rfcxml-elements#front).

Content schema: text

## li
## Tabs {.tabset}
### Usage
A list element, used in [`ol`](/rfcxml-elements#ol) and [`ul`](/rfcxml-elements#ul).

This element can be a child element of [`ol`](/rfcxml-elements#ol) and [`ul`](/rfcxml-elements#ul).

Content schema: ( ( artset | artwork | blockquote | dl | figure | ol | sourcecode | t | table | ul )+ | ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | tt | u | xref )+ )

### Attributes
#### anchor
Document-wide unique identifier for this element.

## link
## Tabs {.tabset}
### Usage
A link to an external document that is related to the RFC.

The following are the supported types of external documents that can be pointed to in a [`link`](/rfcxml-elements#link) element:

The current International Standard Serial Number (ISSN) for the RFC Series. The value for the "rel" attribute is "item". The link should use the form "urn:issn:".
The Digital Object Identifier (DOI) for this document. The value for the "rel" attribute is "describedBy". The link should use the form specified in [RFC7669]; this is expected to change in the future.
The Internet-Draft that was submitted to the RFC Editor to become the published RFC. The value for the "rel" attribute is "prev". (RFC7998 specified "convertedFrom", but that value is not one of the recognised values for the @rel attribute of [`link`](/rfcxml-elements#link) elements in HTML. The "prev" value has the desired semantics.) The link should be to an IETF-controlled web site that retains copies of Internet-Drafts.
A representation of the document offered by the document author. The value for the "rel" attribute is "alternate". The link can be to a personally run web site.
In RFC production mode, the prep tool needs to check the values for [`link`](/rfcxml-elements#link) before an RFC is published. In draft production mode, the prep tool might remove some [`link`](/rfcxml-elements#link) elements during the draft submission process.

This element can be a child element of [`rfc`](/rfcxml-elements#rfc).

### Attributes
#### href (Required)
The URI of the external document.

#### rel
The relationship of the external document to this one. The relationships are taken from the "Link Relations" registry maintained by IANA [LINKRELATIONS].

## middle
## Tabs {.tabset}
### Usage
Represents the main content of the document.

This element can be a child element of [`rfc`](/rfcxml-elements#rfc).

Content schema: section+

## name
## Tabs {.tabset}
### Usage
The name of the containing (parent) element, for instance the section name. This name can include inline markup (for example, including references or making some characters use a fixed-width font).

This element can be a child element of [`figure`](/rfcxml-elements#figure), [`note`](/rfcxml-elements#note), [`references`](/rfcxml-elements#references), [`section`](/rfcxml-elements#section), [`table`](/rfcxml-elements#table), .

Content schema: ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | tt | xref )*

## note
## Tabs {.tabset}
### Usage
Creates an unnumbered, titled block of text that appears after the Abstract.

It is usually used for additional information to reviewers (Working Group information, mailing list, ...) or for additional publication information such as "IESG Notes".

This element can be a child element of [`front`](/rfcxml-elements#front).

Content schema: name?, ( dl | ol | t | ul )+

### Attributes
#### removeInRFC
If set to "true", this note is marked in the prep tool with text indicating that it should be removed before the document is published as an RFC. That text will be "This note is to be removed before publishing as an RFC."

Possible values: ( "true" | "false" )
Default value: "false"

#### title
Deprecated. Use the [`name`](/rfcxml-elements#name) element instead.

## ol
## Tabs {.tabset}
### Usage
An ordered list. The labels on the items will be either a number or a letter, depending on the value of the style attribute.

This element can be a child element of [`abstract`](/rfcxml-elements#abstract), [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), [`note`](/rfcxml-elements#note), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), and [`th`](/rfcxml-elements#th).

Content schema: li+

### Attributes
#### anchor
Document-wide unique identifier for this [`ol`](/rfcxml-elements#ol) element.

#### group
When the prep tool sees an [`ol`](/rfcxml-elements#ol) element with a "group" attribute that has already been seen, it continues the numbering of the list from where the previous list with the same group name left off. If an [`ol`](/rfcxml-elements#ol) element has both a "group" attribute and a "start" attribute, the group's numbering is reset to the given start value.

#### indent
The indentation of the list elements relative to the start of the list item number. With indent='adaptive', the width of the widest list item number will determine the indentation. With a numeric value, that value will be used to determine the amount of indentation. The indentation amount is interpreted as characters when rendering plain-text documents, and en-space units when rendering in formats that have richer typographic support such as HTML or PDF. One en-space is assumed to be the length of 0.5 em-space in CSS units. Only non-negative integer amounts of indentation are supported.

Possible values: ( text | "adaptive" )
Default value: "adaptive"

#### spacing
Defines whether or not there is a blank line between entries. spacing="normal" indicates a single blank line, while spacing="compact" indicates no blank line between entries.

Possible values: ( "normal" | "compact" )
Default value: "normal"

#### start
The ordinal value at which to start the list. This defaults to "1" and must be an integer of value 0 or greater.

Default value: "1"

#### type
The type of the labels on list items. If the length of the type value is 1, the meaning is the same as it is for HTML:

Default value: "1"

a
Lowercase letters (a, b, c, ...)
A
Uppercase letters (A, B, C, ...)
1
Decimal numbers (1, 2, 3, ...)
i
Lowercase Roman numerals (i, ii, iii, ...)
I
Uppercase Roman numerals (I, II, III, ...)
For types "a" and "A", after the 26th entry, the numbering starts at "aa"/"AA", then "ab"/"AB", and so on.

If the length of the type value is greater than 1, the value must contain a percent-encoded indicator and other text. The value is a free-form text that allows counter values to be inserted using a "percent-letter" format. For instance, "[REQ%d]" generates labels of the form "[REQ1]", where "%d" inserts the item number as a decimal number.

The following formats are supported:

%c
Lowercase letters (a, b, c, ...)
%C
Uppercase letters (A, B, C, ...)
%d
Decimal numbers (1, 2, 3, ...)
%i
Lowercase Roman numerals (i, ii, iii, ...)
%I
Uppercase Roman numerals (I, II, III, ...)
%p
The list counter of a list item in a parent list (see more below)
%%
Represents a percent sign
Other formats are reserved for future use. Only one percent encoding other than "%%" and "%p" is allowed in a type string.

It is an error for the type string to be empty. For bulleted lists, use the [`ul`](/rfcxml-elements#ul) element. For lists that have neither bullets nor numbers, use the [`ul`](/rfcxml-elements#ul) element with the 'empty="true"' attribute.

'%p' may be used in nested ordered lists, where it represents the item number of the parent list item. This lets you say for instance:
```xml
<ol>
  <li>List item one</li>
  <li>
    <t>Nested list:</t>
    <ol type='%p%d'>
      <li>Sublist item 2.1</li>
      <li>Sublist item 2.2</li>
    </ol>
  </li>
</ol>
```
which is rendered as:

List item one
Nested list
2.1
Sublist item 2.1
2.2
Sublist item 2.2
Without the '%p' format specifier, you would have to explicitly insert the counter number of the parent item, which could easily result in mismatched numbering if parent list intems were inserted or removed during document editing.

## organization
## Tabs {.tabset}
### Usage
Specifies the affiliation (RFC7322) of an author.

This information appears both in the "Author's Address" section and on the front page (see [RFC7322] for more information). If the value is long, an abbreviated variant can be specified in the "abbrev" attribute.

This element can be a child element of [`author`](/rfcxml-elements#author) and [`contact`](/rfcxml-elements#contact).

Content schema: text

### Attributes
#### abbrev
Abbreviated variant of the organization name.

#### ascii
The ASCII equivalent of the [`organization`](/rfcxml-elements#organization) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

#### asciiAbbrev
The ASCII equivalent of the abbreviated variant of the organization's name.

#### showOnFrontPage
Turns off listing of organization with author name on the first document page.

Possible values: ( "true" | "false" )
Default value: "true"

## phone
## Tabs {.tabset}
### Usage
Represents a phone number.

The value is expected to be the scheme-specific part of a "tel" URI (and so does not include the prefix "tel:"), using the "global-number-digits" syntax. See Section 3 of [RFC3966] for details.

This element can be a child element of [`address`](/rfcxml-elements#address).

Content schema: text

## pobox
## Tabs {.tabset}
### Usage
Represents a post office box number.

This element can be a child element of [`postal`](/rfcxml-elements#postal).

Content schema: text

### Attributes
#### ascii

The ASCII equivalent of the [`pobox`](/rfcxml-elements#pobox) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## postal
## Tabs {.tabset}
### Usage
Contains optional child elements providing postal information. These elements will be displayed in an order that is specific to formatters. A postal address can contain only a set of [`street`](/rfcxml-elements#street), [`city`](/rfcxml-elements#city), [`region`](/rfcxml-elements#region), [`code`](/rfcxml-elements#code), and [`country`](/rfcxml-elements#country) elements, or only an ordered set of [`postalLine`](/rfcxml-elements#postalLine) elements, but not both.

This element can be a child element of [`address`](/rfcxml-elements#address).

Content schema: ( ( city | cityarea | code | country | extaddr | pobox | region | sortingcode | street )* | postalLine+ )

## postalLine
## Tabs {.tabset}
### Usage
Represents one line of a postal address. When more than one [`postalLine`](/rfcxml-elements#postalLine) is given, the prep tool emits them in the order given.

This element can be a child element of [`postal`](/rfcxml-elements#postal).

Content schema: text

#### ascii

The ASCII equivalent of the [`postalLine`](/rfcxml-elements#postalLine) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## refcontent
## Tabs {.tabset}
### Usage
Text that should appear between the title and the date of a reference. The purpose of this element is to obviate the need for abuse of [`seriesInfo`](/rfcxml-elements#seriesInfo) in order to add such text.

For example:
```xml
<reference anchor="April1"> <front> <title>On Being A Fool</title> <author initials="K." surname="Phunny" fullname="Knot Phunny"/> <date year="2000" month="April"/> </front> <refcontent>Self-published pamphlet</refcontent> </reference>
```
would render as:

[April1] Phunny, K., "On Being A Fool", Self-published pamphlet, April 2000.

This element can be a child element of [`reference`](/rfcxml-elements#reference).

Content schema: ( text | bcp14 | em | strong | sub | sup | tt )*

## reference
## Tabs {.tabset}
### Usage
Represents a bibliographic reference.

This element can be a child element of [`referencegroup`](/rfcxml-elements#referencegroup) and [`references`](/rfcxml-elements#references).

Content schema: stream?, front, ( annotation | refcontent | seriesInfo )*

### Attributes
#### anchor (Required)
Document-wide unique identifier for this [`reference`](/rfcxml-elements#reference). Usually, this will be used both to "label" the reference in the "References" section and as an identifier in links to this reference entry; but see [`displayreference`](/rfcxml-elements#displayreference) for how to change this.

#### quote-title
Specifies whether or not the title in the reference should be quoted. This can be used to prevent quoting, such as on errata.

Possible values: ( "true" | "false" )

#### target
Holds the URI for the reference.

## referencegroup
## Tabs {.tabset}
### Usage
Represents a list of bibliographic references that will be represented as a single reference. This is most often used to reference STDs and BCPs, where a single reference (such as "BCP 9") may encompass more than one RFC.

This element can be a child element of [`references`](/rfcxml-elements#references).

Content schema: reference+

### Attributes
#### anchor (Required)
Document-wide unique identifier for this [`referencegroup`](/rfcxml-elements#referencegroup). Usually, this will be used both to "label" the reference group in the "References" section and as an identifier in links to this reference entry; but see [`displayreference`](/rfcxml-elements#displayreference) for how to change this.

#### target
Holds an URI for the reference group, analogous to the "target" attribute of [`reference`](/rfcxml-elements#reference). Useful for a STD which consists of multiple RFCs with their own URLs, but also has its own unique URL.

## references
## Tabs {.tabset}
### Usage
Contains a set of bibliographic references.

In the early days of the RFC Series, there was only one "References" section per RFC. This convention was later changed to group references into two sets, "Normative" and "Informative", as described in [RFC7322]. This vocabulary supports the split with the [`name`](/rfcxml-elements#name) child element. In general, the title should be either "Normative References" or "Informative References".

The recommended way to include references to RFCs and Internet-Drafts is to use the standard XML XInclude mechanism. Here is an example:
```xml
<references>
<name>Normative References</name>
<!--RTP-->
<xi:include href=
"https://xml2rfc.ietf.org/public/rfc/bibxml/reference.RFC.3550.xml"/>
<!--SIP-->
<xi:include href=
"https://xml2rfc.ietf.org/public/rfc/bibxml/reference.RFC.3261.xml"/>
</references>
```
This element can be a child element of [`back`](/rfcxml-elements#back) and [`references`](/rfcxml-elements#references).

Content schema: name?, ( references+ | ( reference | referencegroup )* )

#### anchor
An optional user-supplied identifier for this set of references.

#### title
Deprecated. Use the [`name`](/rfcxml-elements#name) element instead.

## region
## Tabs {.tabset}
### Usage
Provides the region name in a postal address.

This element can be a child element of [`postal`](/rfcxml-elements#postal).

Content schema: text

### Attributes
#### ascii
The ASCII equivalent of the [`region`](/rfcxml-elements#region) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## rfc
## Tabs {.tabset}
### Usage
This is the root element of the xml2rfc vocabulary.

Content schema: link\*, front, middle, back?

### Attributes
#### category
Document category

For RFCs, the "category" attribute determines the "maturity level" (see Section 4 of [RFC2026]). The allowed values are "std" for "Standards Track", "bcp" for "BCP", "info" for "Informational", "exp" for "Experimental", and "historic" for "Historic".

For Internet-Drafts, the "category" attribute is not needed; when supplied, it will appear as "Intended Status". Supplying this information can be useful to reviewers.

Possible values: ( "std" | "bcp" | "exp" | "info" | "historic" )

#### consensus
Affects the generated boilerplate. Note that the values of "no" and "yes" are deprecated and are replaced by "false" and "true".

See RFC7841 for more information.

Possible values: ( "no" | "yes" | "false" | "true" )
Default value: "false"

#### docName
Indicates the draft name (including revision number) for a draft, or the draft from which an RFC derived, for an RFC. Used to insert the `<link rel="prev" href="...">` element that points to the precursor of the RFC, in accordance with the intentions of Section 5.6.3 of RFC7998.

#### indexInclude
Specifies whether or not a formatter is requested to include an index in generated files. If the source file has no [`iref`](/rfcxml-elements#iref) elements, an index is never generated. This option is useful for generating documents where the source document has [`iref`](/rfcxml-elements#iref) elements but the author no longer wants an index.

Possible values: ( "true" | "false" )
Default value: "true"

#### ipr
Represents the Intellectual Property status of the document.

If the attribute is set to the empty string: `<tt>ipr=''</tt>`, it is assumed that this is not a regular IETF/IRTF/IAB/ISE document, and the document header content is reduced. This is considered a feature by a few other standards organisations that have used xml2rfc to format their standards documents.

#### iprExtract
Identifies a single section within the document for which extraction "as is" is explicitly allowed (only relevant for historic values of the "ipr).

#### number
Used to determine wheher to produce an RFC or an Internet-Draft.

#### obsoletes
A comma-separated list of RFC numbers or Internet-Draft names.

The prep tool will parse the attribute value so that incorrect references can be detected.

#### prepTime
The date that the XML was processed by a prep tool. This is included in the XML file just before it is saved to disk. The value is formatted using the "date-time" format defined in Section 5.6 of RFC3339. The "time-offset" should be "Z".

#### seriesNo
Deprecated; instead, use the "value" in [`seriesInfo`](/rfcxml-elements#seriesInfo).

#### sortRefs
Specifies whether or not the prep tool will sort the references in each reference section.

Possible values: ( "true" | "false" )
Default value: "false"

#### submissionType
The document stream, as described in [RFC7841]. (The RFC Series Editor may change the list of allowed values in the future.)

Possible values: ( "IETF" | "IAB" | "IRTF" | "independent" )
Default value: "IETF"

#### symRefs
Specifies whether or not a formatter is requested to use symbolic references (such as "RFC2119"). If the value for this is "false", the references come out as numbers (such as "[3]").

Possible values: ( "true" | "false" )
Default value: "true"

#### tocDepth
Specifies the number of levels of headings that a formatter is requested to include in the table of contents.

Default value: "3"

#### tocInclude
Specifies whether or not a formatter is requested to include a table of contents in generated files.

Possible values: ( "true" | "false" )
Default value: "true"

#### updates
A comma-separated list of RFC numbers or Internet-Draft names.

The prep tool will parse the attribute value so that incorrect references can be detected.

#### version
Specifies the version of xml2rfc syntax used in this document. The only expected value is "3".

## section
## Tabs {.tabset}
### Usage
Represents a section (when inside a [`middle`](/rfcxml-elements#middle) element) or an appendix (when inside a [`back`](/rfcxml-elements#back) element).

Subsections are created by nesting [`section`](/rfcxml-elements#section) elements inside [`section`](/rfcxml-elements#section) elements. Sections are allowed to be empty.

This element can be a child element of [`back`](/rfcxml-elements#back), [`boilerplate`](/rfcxml-elements#boilerplate), [`middle`](/rfcxml-elements#middle), [`section`](/rfcxml-elements#section), and [`toc`](/rfcxml-elements#toc).

Content schema: name?, ( artset | artwork | aside | author | blockquote | contact | dl | figure | iref | ol | sourcecode | t | table | ul )*, section*

### Attributes
#### anchor
Document-wide unique identifier for this [`section`](/rfcxml-elements#section) element.

#### numbered
If set to "false", the formatter is requested to not display a section number. The prep tool will verify that such a section is not followed by a numbered section in this part of the document. Descendant sections of unnumbered sections are unnumbered by definition. Both top-level [`section`](/rfcxml-elements#section)s and other [`section`](/rfcxml-elements#section)s may have numbered='false'.

Possible values: ( "true" | "false" )
Default value: "true"

#### removeInRFC
If set to "true", this section is marked in the prep tool with text indicating that it should be removed before the document is published as an RFC. That text will be "This section is to be removed before publishing as an RFC."

Possible values: ( "true" | "false" )
Default value: "false"

#### title
Deprecated. Use the [`name`](/rfcxml-elements#name) element instead.

#### toc
Indicates to a formatter whether or not the section is to be included in a table of contents, if such a table of contents is produced. This only takes effect if the level of the section would have appeared in the table of contents based on the "tocDepth" attribute of the [`rfc`](/rfcxml-elements#rfc) element, and of course only if the table of contents is being created based on the "tocInclude" attribute of the [`rfc`](/rfcxml-elements#rfc) element. If this is set to "exclude", any section below this one will be excluded as well. The "default" value indicates inclusion of the section if it would be included by the tocDepth attribute of the [`rfc`](/rfcxml-elements#rfc) element.

Possible values: ( "include" | "exclude" | "default" )
Default value: "default"

## seriesInfo
## Tabs {.tabset}
### Usage
Specifies the document series in which this document appears, and also specifies an identifier within that series.

A processing tool determines whether it is working on an RFC or an Internet-Draft by inspecting the "name" attribute of a [`seriesInfo`](/rfcxml-elements#seriesInfo) element inside the [`front`](/rfcxml-elements#front) element inside the [`rfc`](/rfcxml-elements#rfc) element, looking for "RFC" or "Internet-Draft". (Specifying neither value in any of the [`seriesInfo`](/rfcxml-elements#seriesInfo) elements can be useful for producing other types of documents but is out of scope for this specification.)

It is invalid to have multiple [`seriesInfo`](/rfcxml-elements#seriesInfo) elements inside the same [`front`](/rfcxml-elements#front) element containing the same "name" value. Some combinations of [`seriesInfo`](/rfcxml-elements#seriesInfo) "name" attribute values make no sense, such as having both `<seriesInfo name="rfc"/>` and `<seriesInfo name="Internet-Draft"/>` in the same [`front`](/rfcxml-elements#front) element.

This element can be a child element of [`front`](/rfcxml-elements#front) and [`reference`](/rfcxml-elements#reference).

Content schema: empty

### Attributes
#### asciiName
The ASCII equivalent of the name field.

#### asciiValue
The ASCII equivalent of the value field.

#### name (Required)
The name of the series. Some values in use by the IETF community are "RFC", "Internet-Draft", and "DOI", but other names such as "ISO", "W3C" for exist for other standardisation organisations.

#### status
TBD

#### stream
Deprecated. Use the [`stream`](/rfcxml-elements#stream) element instead.

Possible values: ( "IETF" | "IAB" | "IRTF" | "independent" )

#### value (Required)

The identifier within the series specified by the "name" attribute.

For BCPs, FYIs, RFCs, and STDs, this is the number within the series.

For Internet-Drafts, it is the full draft name (ending with the two-digit version number).

For DOIs, the value is given, such as "10.17487/rfc1149", as described in [RFC7669].

The name in the value should be the document name without any file extension.

## sortingcode
## Tabs {.tabset}
### Usage
A sorting code is related to postal codes in that it is used in addresses to allow sorting, for example to route mail to a certain postal centre or to distinguish streets with the same name in two different areas of the same settlement.

This element can be a child element of [`postal`](/rfcxml-elements#postal).

Content schema: text

### Attributes
#### ascii

The ASCII equivalent of the [`sortingcode`](/rfcxml-elements#sortingcode) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## sourcecode
## Tabs {.tabset}
### Usage
This element allows the inclusion of source code into the document.

When rendered, source code is always shown in a monospace font. When [`sourcecode`](/rfcxml-elements#sourcecode) is a child of [`figure`](/rfcxml-elements#figure) or [`section`](/rfcxml-elements#section), it provides full control of horizontal whitespace and line breaks. When formatted, it is indented relative to the left margin of the enclosing element. It is thus useful for source code and formal languages, such as ABNF (RFC5234) or the RNC notation used in this document. (When [`sourcecode`](/rfcxml-elements#sourcecode) is a child of other elements, it flows with the text that surrounds it.) Tab characters (U+0009) inside of this element are prohibited.

For artwork such as character-based art, diagrams of message layouts, and so on, use the [`artwork`](/rfcxml-elements#artwork) element instead.

Output formatters that do pagination will attempt to keep source code on a single page. This is to prevent source code that is split across pages from looking like two separate pieces of code.

This element can be a child element of [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`figure`](/rfcxml-elements#figure), [`li`](/rfcxml-elements#li), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), and [`th`](/rfcxml-elements#th).

Content schema: text

### Attributes
#### anchor
Document-wide unique identifier for this [`sourcecode`](/rfcxml-elements#sourcecode) element.

#### markers
Indicates whether `<CODE BEGINS>` and `<CODE ENDS>` markers, as introduced by [RFC6087], should be generated when rendering the [`sourcecode`](/rfcxml-elements#sourcecode) element. The alternative is to include these explicitly inside the element, but that would necessitate extra code to strip these, when extracting code from the XML source.

Possible values: ( "true" | "false" )
Default value: "false"

#### name
A filename suitable for the contents (such as for extraction to a local file). This attribute can be helpful for other kinds of tools (such as automated syntax checkers, which work by extracting the source code). Note that the "name" attribute does not need to be unique for [`artwork`](/rfcxml-elements#artwork) elements in a document. If multiple [`sourcecode`](/rfcxml-elements#sourcecode) elements have the same "name" attribute, a formatter might assume that the elements are all fragments of a single file, and such a formatter can collect those fragments for later processing.

#### src
The URI reference of a source file (RFC3986).

It is an error to have both a "src" attribute and content in the [`sourcecode`](/rfcxml-elements#sourcecode) element.

#### type
Specifies the type of the source code. The value of this attribute is free text with certain values designated as preferred.

Most of the preferred values for [`sourcecode`](/rfcxml-elements#sourcecode) types are language names, in a wide sense, such as "abnf", "asn.1", "bash", "c++", etc.

The RFC Series Editor maintains a list of the preferred values on the RFC Editor web site at https://www.rfc-editor.org/materials/sourcecode-types.txt, and that list is updated over time. Thus, a consumer of v3 XML should not cause a failure when it encounters an unexpected type or no type is specified.

## stream
## Tabs {.tabset}
### Usage
Indicates which stream an RFC belongs to.

This element can be a child element of [`reference`](/rfcxml-elements#reference).

Content schema: ( "IETF" | "IAB" | "IRTF" | "independent" )?

## street
## Tabs {.tabset}
### Usage
Provides a street address.

This element can be a child element of [`postal`](/rfcxml-elements#postal).

Content schema: text

### Attributes
#### ascii
The ASCII equivalent of the [`street`](/rfcxml-elements#street) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## strong
## Tabs {.tabset}
### Usage
Indicates text that is semantically strong. In HTML and PDF rendering, text enclosed within this element will be displayed as bold after processing; in text rendering it will be preceeded and followed by an asterisk. This element can be combined with other character formatting elements, and the formatting will be additive.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`refcontent`](/rfcxml-elements#refcontent), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt), and [`xref`](/rfcxml-elements#xref).

Content schema: ( text | bcp14 | br | cref | em | eref | iref | sub | sup | tt | xref )*

## sub
## Tabs {.tabset}
### Usage
Causes the text to be displayed as subscript, approximately half a letter-height lower than normal text, in HTML and PDF rendering. This element can be combined with other character formatting elements, and the formatting will be additive.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`refcontent`](/rfcxml-elements#refcontent), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt), and [`xref`](/rfcxml-elements#xref).

Content schema: ( text | bcp14 | cref | em | eref | iref | strong | sub | sup | tt | xref )*

## sup
## Tabs {.tabset}
### Usage
Causes the text to be displayed as superscript, approximately half a letter-height higher than normal text, in HTML and PDF rendering. This element can be combined with other character formatting elements, and the formatting will be additive.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`refcontent`](/rfcxml-elements#refcontent), [`strong`](rfcxml-elements[`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt), and [`xref`](/rfcxml-elements#xref).

Content schema: ( text | bcp14 | cref | em | eref | iref | strong | sub | sup | tt | xref )*

## t
## Tabs {.tabset}
### Usage
Contains a paragraph of text.

This element can be a child element of [`abstract`](/rfcxml-elements#abstract), [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), [`note`](/rfcxml-elements#note), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), and [`th`](/rfcxml-elements#th).

Content schema: ( text | bcp14 | br | contact | cref | em | eref | iref | strong | sub | sup | tt | u | xref )*

### Attributes
#### anchor
Document-wide unique identifier for this paragraph.

#### hangText
Deprecated. Instead, use [`dd`](/rfcxml-elements#dd) inside of a definition list ([`dl`](/rfcxml-elements#dl)).

#### indent
Indicates any extra amount of indentation to be used when rendering the paragraph of text. The indentation amount is interpreted as characters when rendering plain-text documents, and en-space units when rendering in formats that have richer typographic support such as HTML or PDF. One en-space is assumed to be the length of 0.5 em-space in CSS units. Only non-negative integer amounts of indentation are supported.

Default value: "0"

#### keepWithNext
Acts as a hint to the output formatters that do pagination to do a best-effort attempt to keep the paragraph with the next element, whatever that happens to be. For example, for HTML output @media print CSS might translate this to page-break-after: avoid. For PDF, the paginator could attempt to keep the paragraph with the next element. Note: this attribute is strictly a hint and not always actionable.

Possible values: ( "true" | "false" )
Default value: "false"

#### keepWithPrevious
Acts as a hint to the output formatters that do pagination to do a best-effort attempt to keep the paragraph with the previous element, whatever that happens to be. For example, for HTML output @media print CSS might translate this to page-break-before: avoid. For PDF, the paginator could attempt to keep the paragraph with the previous element. Note: this attribute is strictly a hint and not always actionable.

Possible values: ( "true" | "false" )
Default value: "false"

## table
## Tabs {.tabset}
### Usage
Contains a table with a caption with the table number. If the element contains a [`name`](/rfcxml-elements#name) element, the caption will also show that name.

Inside the [`table`](/rfcxml-elements#table) element there is, optionally, a [`thead`](/rfcxml-elements#thead) element to contain the rows that will be the table's heading and, optionally, a [`tfoot`](/rfcxml-elements#tfoot) element to contain the rows of the table's footer. If the XML is converted to a representation that has page breaks (such as PDFs or printed HTML), the header and footer are meant to appear on each page.

This element can be a child element of [`aside`](/rfcxml-elements#aside), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), and [`section`](/rfcxml-elements#section).

Content schema: name?, iref\*, thead?, tbody+, tfoot?

### Attributes
#### align
Controls whether the table appears left justified, centered, or right justified. The caption will be centered under the table, and the combined table and caption will be aligned according to the "align" attribute.

Possible values: ( "left" | "center" | "right" )
Default value: "center"

#### anchor
Document-wide unique identifier for this element.

## tbody
## Tabs {.tabset}
### Usage
A container for a set of body rows for a table.

This element can be a child element of [`table`](/rfcxml-elements#table).

Content schema: tr+

#### anchor
Document-wide unique identifier for this element.

## td
## Tabs {.tabset}
### Usage
A cell in a table row.

This element can be a child element of [`tr`](/rfcxml-elements#tr).

Content schema: ( ( artset | artwork | dl | figure | ol | sourcecode | t | ul )+ | ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | tt | u | xref )* )

### Attributes
#### align
Controls whether the content of the cell appears left justified, centered, or right justified. Note that "center" or "right" will probably only work well in cells with plain text; any other elements might make the contents render badly.

Possible values: ( "left" | "center" | "right" )
Default value: "left"

#### anchor
Document-wide unique identifier for this element.

#### colspan
The number of columns that the cell is to span. For example, setting "colspan='3'" indicates that the cell occupies the same horizontal space as three cells of a row without any "colspan" attributes.

Default value: "1"

#### rowspan
The number of rows that the cell is to span. For example, setting "rowspan='3'" indicates that the cell occupies the same vertical space as three rows.

Default value: "1"

## tfoot
## Tabs {.tabset}
### Usage
A container for a set of footer rows for a table.

This element can be a child element of [`table`](/rfcxml-elements#table).

Content schema: tr+

### Attributes
#### anchor
Document-wide unique identifier for this element.

## th
## Tabs {.tabset}
### Usage
A cell in a table row. When rendered, this will normally come out in boldface; other than that, there is no difference between this and the [`td`](rfcxml-elements#td) element.

This element can be a child element of [`tr`](/rfcxml-elements#tr).

Content schema: ( ( artset | artwork | dl | figure | ol | sourcecode | t | ul )+ | ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | tt | u | xref )* )

#### align
Controls whether the content of the cell appears left justified, centered, or right justified. Note that "center" or "right" will probably only work well in cells with plain text; any other elements might make the contents render badly.

Possible values: ( "left" | "center" | "right" )
Default value: "left"

#### anchor
Document-wide unique identifier for this element.

#### colspan
The number of columns that the cell is to span. For example, setting "colspan='3'" indicates that the cell occupies the same horizontal space as three cells of a row without any "colspan" attributes.

Default value: "1"

#### rowspan
The number of rows that the cell is to span. For example, setting "rowspan='3'" indicates that the cell occupies the same vertical space as three rows.

Default value: "1"

## thead
## Tabs {.tabset}
### Usage
A container for a set of header rows for a table.

This element can be a child element of [`table`](/rfcxml-elements#table).

Content schema: tr+

### Attributes
#### anchor
Document-wide unique identifier for this element.

## title
## Tabs {.tabset}
### Usage
Represents the document title.

When this element appears in the [`front`](/rfcxml-elements#front) element of the current document, the title might also appear in page headers or footers. If it is long (\~40 characters), the "abbrev" attribute can be used to specify an abbreviated variant.

This element can be a child element of [`front`](/rfcxml-elements#front).

Content schema: ( text | br )*

#### abbrev
Specifies an abbreviated variant of the document title.

#### ascii
The ASCII equivalent of the [`title`](/rfcxml-elements#title) content. This element may have non-ASCII Latin script content without specifying an ASCII equivalent, but for other non-ASCII content an ASCII equivalent is required.

## toc
## Tabs {.tabset}
### Usage
This element contains the Table of Content. The content of the [`toc`](/rfcxml-elements#toc) element is generated by the preptool based on the "tocInclude" and "tocDepth" attributes of the [`rfc`](/rfcxml-elements#rfc) element. As a document author, you should not use [`toc`](/rfcxml-elements#toc) directly.

This element can be a child element of [`front`](/rfcxml-elements#front).

Content schema: section*

## tr
## Tabs {.tabset}
### Usage
A row of a table.

This element can be a child element of [`tbody`](/rfcxml-elements#tbody), [`tfoot`](/rfcxml-elements#tfoot), and [`thead`](/rfcxml-elements#thead).

Content schema: ( td | th )+

### Attributes
#### anchor
Document-wide unique identifier for this element.

## tt
## Tabs {.tabset}
### Usage
Causes the text to be displayed in a constant-width font. This element can be combined with other character formatting elements, and the formatting will be additive.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`refcontent`](/rfcxml-elements#refcontent), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), and [`xref`](/rfcxml-elements#xref).

Content schema: ( text | bcp14 | br | cref | em | eref | iref | strong | sub | sup | xref )*

## u
## Tabs {.tabset}
### Usage
The elements [`author`](/rfcxml-elements#author), [`organisation`](/rfcxml-elements#organisation), [`street`](/rfcxml-elements#street), [`city`](/rfcxml-elements#city), [`region`](/rfcxml-elements#region), [`code`](/rfcxml-elements#code), [`country`](/rfcxml-elements#country), [`postalLine`](/rfcxml-elements#postalLine), [`email`](/rfcxml-elements#email), [`seriesInfo`](/rfcxml-elements#seriesInfo), and [`title`](/rfcxml-elements#title) may contain non- ascii characters for the purpose of rendering author names, addresses, and reference titles correctly. They also have an additional "ascii" attribute for the purpose of proper rendering in ascii-only media.

In order to insert Unicode characters in any other context, xml2rfc vocabulary v3 requires that the Unicode string be enclosed within an [`u`](/rfcxml-elements#u) element. The element will be expanded inline based on the value of a "format" attribute. This provides a generalised means of generating the 6 methods of Unicode renderings listed in [RFC7997], Section 3.4, and also several others found in for instance the RFC Format Tools example rendering of RFC 7700, at https://rfc-format.github.io/draft-iab-rfc-css-bis/sample2-v2.html.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), and [`th`](/rfcxml-elements#th).

Content schema: text

### Attributes
#### anchor
Document-wide unique identifier for this element.

#### ascii
The ASCII equivalent of the content, to be used if the "ascii" keyword is used in the "format" specification.

#### format
The "format" attribute accepts either a simplified format specification, or a full format string with placeholders for the various possible Unicode expansions.

The simplified format consists of dash-separated keywords, where each keyword represents a possible expansion of the Unicode character or string; use for example `<u "lit-num-name">foo</u>` to expand the text to its literal value, code point values, and code point names.

A combination of up to 3 of the following keywords may be used, separated by dashes: "num", "lit", "name", "ascii", "char". The keywords are expanded as follows and combined, with the second and third enclosed in parentheses if present:

* "ascii" - The value of the 'ascii' attribute on the [`u`](/rfcxml-elements#u) element
* "char" - The literal element text, without quotes
* "lit" - The literal element text, enclosed in quotes
* "name" - The Unicode name(s) of the element text
* "num" - The numeric value(s) of the element text, in U+1234 notation

In order to ensure that no specification mistakes can result for rendering methods that cannot render all Unicode code points, "num" MUST always be part of the specified format.

Default value: "lit-name-num"

##### Examples
* format="num-lit": `Temperature changes are indicated by the character U+0394 ("Δ")`
* format="num-name": `Temperature changes are indicated by the character U+0394 (GREEK CAPITAL LETTER DELTA)`
* format="num-lit-name": `Temperature changes are indicated by the character U+0394 ("Δ", GREEK CAPITAL LETTER DELTA)`
* format="num-name-lit": `Temperature changes are indicated by the character U+0394 (GREEK CAPITAL LETTER DELTA, "Δ")`
* format="name-lit-num": `Temperature changes are indicated by the character GREEK CAPITAL LETTER DELTA ("Δ", U+0394)`
* format="lit-name-num": `Temperature changes are indicated by the character "Δ" (GREEK CAPITAL LETTER DELTA, U+0394)`

##### Expansion of [`u`](/rfcxml-elements#u) multi-codepoint strings

If the [`u`](/rfcxml-elements#u) element encloses a sequence of Unicode codepoints, rather than a single one, the rendering reflects this. For example:
```xml
   <u format="num-lit">ᏚᎢᎵᎬᎢᎬᏒ</u>
```
will be expanded to "U+13DA U+13A2 U+13B5 U+13AC U+13A2 U+13AC U+13D2 ("ᏚᎢᎵᎬᎢᎬᏒ")".

Unicode characters in document text which are not enclosed in [`u`](/rfcxml-elements#u) will be replaced with a question mark (?) and a warning will be issued.

##### Non-simplified [`u`](rfcxml-elements#u) format specifications
In order to provide for cases where the simplified format above is insufficient, without relinquishing the requirement that the number of a code point always must be rendered, the "format" attribute can also accept a full format string. This format uses placeholders which consist of any of the key words above enclosed in curly braces; outside of this, any ascii text is permissible. For example,

```xml
   The <u format="{lit} character ({num})">Δ</u>
```
will be rendered as

```
   The "Δ" character (U+0394).
```

As for the simplified format, "num" MUST always be part of the specified format in order to ensure that no specification mistakes can result for rendering methods that cannot render all Unicode code points,

###### Split expansion of [`u`](rfcxml-elements#u) elements

There are cases which cannot be handled with either the simplified or full [`u`](/rfcxml-elements#u) format specifications. One is exemplified in Table 1 of the CSS sample document at https://rfc-format.github.io/draft-iab-rfc-css-bis/sample2-v2.html#s-3. Rendering this with [`u`](/rfcxml-elements#u) elements requires that the non-ascii content be rendered in one place (a table cell in one column) while the expansion is rendered in another cell in a different column. Provision for this has been made by modifying the expansion of [`u`](/rfcxml-elements#u) when it is referenced by an [`xref`](/rfcxml-elements#xref). This table, with [`u`](/rfcxml-elements#u) elements referenced by [`xref`](/rfcxml-elements#xref) instances:
```xml
   <table>
     <name>A Sample of Legal Nicknames</name>
     <thead>
       <tr>
          <th>#</th>
          <th>Nickname</th>
          <th>Output for comparison</th>
       </tr>
     </thead>
     <tbody>
       <tr>
          <td>1</td>
          <td>&lt;Foo&gt;</td>
          <td>&lt;foo&gt;</td>
       </tr>
       <tr>
          <td>2</td>
          <td>&lt;foo&gt;</td>
          <td>&lt;foo&gt;</td> </tr>
       <tr>
          <td>3</td>
          <td>&lt;Foo Bar&gt;</td>
          <td>&lt;foo bar&gt;</td>
       </tr>
       <tr>
          <td>4</td>
          <td>&lt;foo bar&gt;</td>
          <td>&lt;foo bar&gt;</td>
       </tr>
       <tr>
         <td>5</td>
         <td>
            &lt;
            <u format="name-num" anchor="greek-upper-sigma">Σ</u>
            &gt;
         </td>
         <td> <xref target="greek-upper-sigma" /> </td>
       </tr>
       <tr>
          <td>6</td>
          <td>
             &lt;
             <u format="name-num" anchor="greek-lower-sigma">σ</u>
             &gt;
          </td>
          <td> <xref target="greek-lower-sigma" /> </td>
       </tr>
       <tr>
          <td>7</td>
          <td>
             &lt;
             <u format="name-num" anchor="greek-final-sigma">ς</u>
             &gt;
          </td>
          <td> <xref target="greek-final-sigma" /> </td>
       </tr>
       <tr>
          <td>8</td>
          <td>
             &lt;
             <u format="name-num" anchor="black-chess-king">♚</u>
             &gt;
          </td>
          <td>
             <xref target="black-chess-king" format="default"/>
          </td>
       </tr>
       <tr>
          <td>9</td>
          <td>
             &lt;Richard
             <u format="{char}> ({num})" anchor="richard-iv">Ⅳ</u>
             &gt;
          </td>
          <td>&lt;richard iv&gt;</td>
       </tr>
     </tbody>
   </table>
```
comes out as shown below:

| #   | Nickname               | Output for comparison                   |
| --: | :--------------------- | :-------------------------------------- |
| 1   | \<Foo\>                | \<foo\>                                 |
| 2   | \<foo\>                | \<foo\>                                 |
| 3   | \<Foo Bar\>            | \<foo bar\>                             |
| 4   | \<foo bar\>            | \<foo bar\>                             |
| 5   | \<Σ\>                  | GREEK CAPITAL LETTER SIGMA (U+03A3)     |
| 6   | \<σ\>                  | GREEK SMALL LETTER SIGMA (U+03C3)       |
| 7   | \<ς\>                  | GREEK SMALL LETTER FINAL SIGMA (U+03C2) |
| 8   | \<♚\>                  | BLACK CHESS KING (U+265A)               |
| 9   | \<Richard Ⅳ\> (U+2163) | \<richard iv\>                          |
_Table 1: A Sample of Legal Nicknames_


## ul
## Tabs {.tabset}
### Usage
An unordered list. The labels on the items will be symbols picked by the formatter.

This element can be a child element of [`abstract`](/rfcxml-elements#abstract), [`aside`](/rfcxml-elements#aside), [`blockquote`](/rfcxml-elements#blockquote), [`dd`](/rfcxml-elements#dd), [`li`](/rfcxml-elements#li), [`note`](/rfcxml-elements#note), [`section`](/rfcxml-elements#section), [`td`](/rfcxml-elements#td), and [`th`](/rfcxml-elements#th).

Content schema: li+

### Attributes
#### anchor
Document-wide unique identifier for this element.

#### bare
Can only be used with empty="true" (see below). Determines if the blank bullet has an horizontal extension or not. With bare="false", the empty list bullet will still occupy the same space as for empty="false". With empty="true", there will be no bullet at all, i.e., the list items will have no indentation.

Possible values: ( "true" | "false" )
Default value: "false"

Example: an unordered list with bare="true" and empty="true":

One
Two

#### empty
Defines whether or not the list item bullets are empty. empty="true" indicates that a blank (empty) bullet will be shown.

Possible values: ( "true" | "false" )
Default value: "false"

Example: an unordered list with bare="false" and empty="false":

* One
* Two

Example: an unordered list with bare="false" and empty="true":

  One
  Two

#### indent
The indentation of the list elements relative to the start of the bullet or bullet text.

Default value: "3"

#### spacing
Defines whether or not there is a blank line between entries. spacing="normal" indicates a single blank line, while spacing="compact" indicates no blank line between entries.

Possible values: ( "normal" | "compact" )
Default value: "normal"

## uri
## Tabs {.tabset}
### Usage
Contains a web address associated with the author.

The contents should be a valid URI; this most likely will be an "http:" or "https:" URI.

This element can be a child element of [`address`](/rfcxml-elements#address).

Content schema: text

## workgroup
## Tabs {.tabset}
### Usage
This element is used to specify the Working Group (IETF) or Research Group (IRTF) from which the document originates, if any. The recommended format is the official name of the Working Group (with some capitalization).

In Internet-Drafts, this is used in the upper left corner of the boilerplate, replacing the "Network Working Group" string. Formatting software can append the words "Working Group" or "Research Group", depending on the "submissionType" property of the [`rfc`](/rfcxml-elements#rfc) element.

This element can be a child element of [`front`](/rfcxml-elements#front).

Content schema: text

## xref
## Tabs {.tabset}
### Usage
A reference to an anchor in this document. Formatters that have links (such as HTML and PDF) are likely to render [`xref`](/rfcxml-elements#xref) elements as internal hyperlinks. This element is useful for referring to references in the "References" section, to specific sections of the document, to specific figures, and so on.

If the "section" attribute is present, this represents a link to a specific part of a document that appears in a [`reference`](/rfcxml-elements#reference) element. Formatters that have links (such as HTML and PDF) render [`xref`](/rfcxml-elements#xref) elements with "section" attributes as external hyperlinks to the specified part of the reference, creating the link target by combining the base URI from the [`reference`](/rfcxml-elements#reference) element with the "relative" attribute from this element. The "target" attribute is required, and it must be the anchor of a [`reference`](/rfcxml-elements#reference) element.

If the reference is not an RFC or Internet-Draft that is in the v3 format, the element needs to have a "relative" attribute; in this case, the value of the "section" attribute is used to render the text of the external link.

If the "sectino" attribute is present, the rendering will for most cominations of the "format" and "sectionFormat" have two links; one external link to the specific part of the referenced document, and one internal link to the [`reference`](/rfcxml-elements#reference) entry.

The attribute "format" affect the internal link rendering only, and the "sectionFormat" affects the rendering of the external link and its textual relationship to the internal link only.

This element can be a child element of [`annotation`](/rfcxml-elements#annotation), [`blockquote`](/rfcxml-elements#blockquote), [`cref`](/rfcxml-elements#cref), [`dd`](/rfcxml-elements#dd), [`dt`](/rfcxml-elements#dt), [`em`](/rfcxml-elements#em), [`li`](/rfcxml-elements#li), [`name`](/rfcxml-elements#name), [`strong`](/rfcxml-elements#strong), [`sub`](/rfcxml-elements#sub), [`sup`](/rfcxml-elements#sup), [`t`](/rfcxml-elements#t), [`td`](/rfcxml-elements#td), [`th`](/rfcxml-elements#th), [`tt`](/rfcxml-elements#tt).

Content schema: ( text | em | strong | sub | sup | tt )*

### Attributes
#### format
Possible values: ( "default" | "title" | "counter" | "none" )
Default value: "default"

This attribute signals to formatters what the desired format of the internal link to the relevant [`reference`](/rfcxml-elements#reference) should be.

* "default" - If the element has no content, the "derivedContent" attribute will contain a text fragment that describes the referenced part completely, such as "XML" for a target that is a [`reference`](/rfcxml-elements#reference), or "Section 2" or "Table 4" for a target to a non-reference.

* "title" - If the target is a [`reference`](/rfcxml-elements#reference) element, the "derivedContent" attribute will contain the name of the reference, extracted from the [`title`](/rfcxml-elements#title) child of the [`front`](/rfcxml-elements#front) child of the reference. Or, if the target element has a [`name`](/rfcxml-elements#name) child element, the "derivedContent" attribute will contain the text content of that [`name`](/rfcxml-elements#name) element concatenated with the text content of each descendant node of [`name`](/rfcxml-elements#name) (that is, stripping out all of the XML markup, leaving only the text). Or, if the target element does not contain a [`name`](/rfcxml-elements#name) child element, the "derivedContent" attribute will contain the name of the "anchor" attribute of that element with no other adornment.

* "counter" - The "derivedContent" attribute will contain just a counter. This is used for targets that are [`section`](/rfcxml-elements#section), [`figure`](/rfcxml-elements#figure), [`table`](/rfcxml-elements#table), or items in an ordered list. Using "format='counter'" where the target is any other type of element is an error.

* "none" - There will be no autogenerated text for the xref. When this value is used, it expected that the [`xref`](/rfcxml-elements#xref) element will have explicit text content.

#### relative
Specifies a relative reference from the URI in the target reference. This value must include whatever leading character is needed to create the relative reference; typically, this is "#" for HTML documents.

#### section
Specifies a section of the target reference. If the reference is not an RFC or Internet-Draft in the v3 format, and no "relative" attribute has been provided, it is an error.

#### sectionFormat
Possible values: ( "of" | "comma" | "parens" | "bare" )
Default value: "of"

This attribute is used to signal formatters what the desired format of the external reference should be. Formatters for document types that have linking capability should wrap each part of the displayed text in hyperlinks. If there is content in the [`xref`](/rfcxml-elements#xref) element, that content will be used when rendering the internal link part of the [`xref`](/rfcxml-elements#xref) rendering, but will not affect the external link.

* "of" - The [`xref`](/rfcxml-elements#xref) element will be displayed as an external link followed by an internal link, separated by the work 'of'. The external link will have as its display text the word "Section" followed by a space and the contents of the "section" attribute. This will be followed by a space, the word "of", another space, and an internal link to the relevant [`reference`](/rfcxml-elements#reference) entry, formatted based on the "format" attribute.

* "comma" - The [`xref`](/rfcxml-elements#xref) element will be displayed as an internal link followed by an external link, separated by a comma. The external link will have as its display text the word "Section" followed by a space and the contents of the "section" attribute. The internal link will point to the relevant [`reference`](/rfcxml-elements#reference) entry, and will be rendered according to the "format" attribute.

* "parens" - The [`xref`](/rfcxml-elements#xref) element will be displayed as an internal link followed by an external link within parentheses. The external link will have as its display text the word "Section" followed by a space and the contents of the "section" attribute. The internal link will point to the relevant [`reference`](/rfcxml-elements#reference) entry, and will be rendered according to the "format" attribute.

* "bare" - The [`xref`](/rfcxml-elements#xref) element will be displayed as an external link, possibly followed by the same link within parentheses. The first external link will have as its display text only contents of the "section" attribute; the second link will be present within parentheses only if the [`xref`](/rfcxml-elements#xref) element has any text content, and will then have the text content as its display text.

This value for the "sectionFormat" attribute is useful when it is desired to express for instance "Sections 3.2 and 3.3 of [RFC7997]".

#### target (Required)
Identifies the document component being referenced. The value needs to match the value of the "anchor" attribute of an element in the document; otherwise, it is an error.