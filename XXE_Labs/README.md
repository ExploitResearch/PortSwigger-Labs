# XML External Entity (XXE) Injection

[https://h3x0s3.github.io/PortSwigger-XML-external-external-(XXE)-injection-Labs-&-Notes-Writeup/](https://h3x0s3.github.io/PortSwigger-XML-external-external-(XXE)-injection-Labs-&-Notes-Writeup/)

### XML

XML (eXtensible Markup Language) is a markup language that defines a set of rules for encoding documents in a format that is both human-readable and machine-readable. It is a markup language used for storing and transporting data.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--Above the line is called XML prolog and it specifies the XML version and the encoding used in the XML document. This line is not compulsory to use but it is considered a `good practice` to put that line in all your XML documents.-->
<mail>
<to>falcon</to>
<from>feast</from>
<subject>About XXE</subject>
<text>Teach about XXE</text>
</mail>
<!-- The <mail> is the ROOT element of that document and <to>, <from>, <subject>, <text> are the children elements. -->
```

XML is a case sensitive language. If a tag starts like `<to>` then it has to end by `</to>` and not by something like `</To>`(notice the capitalization of `T`)

Every XML document must contain a `ROOT` element. If the XML document doesn't have any root element then it would be considered `wrong` or `invalid` XML doc.

### DTD

A DTD is a Document Type Definition. It defines the structure and the legal elements and attributes of an XML document.

Internal DTD

```bash
<!DOCTYPE person [
  <!ELEMENT person (name, age, address)>
  <!ELEMENT name (#PCDATA)>
  <!ELEMENT age (#PCDATA)>
  <!ELEMENT address (street, city, state, zip)>
  <!ELEMENT street (#PCDATA)>
  <!ELEMENT city (#PCDATA)>
  <!ELEMENT state (#PCDATA)>
  <!ELEMENT zip (#PCDATA)>
]>

<person>
  <name>John Doe</name>
  <age>30</age>
  <address>
    <street>123 Main St</street>
    <city>Anytown</city>
    <state>CA</state>
    <zip>12345</zip>
  </address>
</person>
```

External DTD

```bash
<!DOCTYPE person SYSTEM "note.dtd">
<person>
  <name>John Doe</name>
  <age>30</age>
  <address>
    <street>123 Main St</street>
    <city>Anytown</city>
    <state>CA</state>
    <zip>12345</zip>
  </address>
</person>
```

we have a file named `note.dtd` with the following content:

```bash
<!DOCTYPE person [
  <!ELEMENT person (name, age, address)>
  <!ELEMENT name (#PCDATA)>
  <!ELEMENT age (#PCDATA)>
  <!ELEMENT address (street, city, state, zip)>
  <!ELEMENT street (#PCDATA)>
  <!ELEMENT city (#PCDATA)>
  <!ELEMENT state (#PCDATA)>
  <!ELEMENT zip (#PCDATA)>
]>
```

**!DOCTYPE person** defines that the root element of this document is person
**!ELEMENT person** defines that the person element must contain three elements: ` name, age, address`
**!ELEMENT name **defines the name element to be of type “#PCDATA”

The syntax for having attributes is also very similar to HTML.

```bash
<text category = "message">You need to learn about XXE</text>
```

In the above example `category` is the attribute name and `message` is the attribute value.

## Labs

- [Blind XXE with out-of-band interaction](./Blind_XXE_with_out-of-band_interaction.md)
- [Blind XXE with out-of-band interaction via XML parameter entities](./Blind_XXE_with_out-of-band_interaction_via_XML_parameter_entities.md)
- [Exploiting XInclude to retrieve files](./Exploiting_XInclude_to_retrieve_files.md)
- [Exploiting XXE to perform SSRF attacks](./Exploiting_XXE_to_perform_SSRF_attacks.md)
- [Exploiting XXE to retrieve data by repurposing a local DTD](./Exploiting_XXE_to_retrieve_data_by_repurposing_a_local_DTD.md)
- [Exploiting XXE using external entities to retrieve files](./Exploiting_XXE_using_external_entities_to_retrieve_files.md)
- [Exploiting XXE via image file upload](./Exploiting_XXE_via_image_file_upload.md)
- [Exploiting blind XXE to exfiltrate data using a malicious external DTD](./Exploiting_blind_XXE_to_exfiltrate_data_using_a_malicious_external_DTD.md)
- [Exploiting blind XXE to retrieve data via error messages](./Exploiting_blind_XXE_to_retrieve_data_via_error_messages.md)
