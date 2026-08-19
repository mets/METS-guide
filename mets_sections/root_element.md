---
title: METS root element
parent: Sections of a METS Document
nav_order: 1
---
# METS root element

The root element `<mets>` defines the container for the information to be stored and/or transmitted by the standard.

```xml
<mets:mets OBJID="loc.natlib.ihas.200003790"
    PROFILE="http://www.loc.gov/mets/profiles/00000007.xml"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      http://www.loc.gov/standards/mets/mets.xsd">
```

## Elements contained in the root element

The METS document structure consists of four major sections, which in turn may contain a variety of elements and attributes as specified in the METS schema.

At the most general level, a METS document may contain the following sections, each of which is described in a separate section of this chapter.

* [METS header - metsHdr](metsHdr.md) -- The METS header contains metadata describing the METS document itself, including information such as creator, editor, etc.

* [Metadata section - mdSec](mdSec.md) -- This section contains metadata that is external to the METS document, internally embedded metadata, or both. Multiple instances of both external and internal metadata can be included in the metadata section. For example, the metadata section may contain descriptive metadata, information about how the files were created and stored, intellectual property rights, metadata about the original source object from which the digital object was derived, information about the provenance of the files that comprise the object (i.e., master/derivative file relationships, and migration/transformation information).

* [File section - fileSec](fileSec.md) -- A list of all files containing content that make up the electronic versions of the digital object. File elements may be grouped within file group elements, to allow for subdivision of files by object version or other criteria such as file type, size, etc.

* [Structure section - structSec](structSec.md) -- The structure section outlines a hierarchical structure for the digital object, and links the elements of that structure to the content files and metadata associated with each element.

## METS root element example

This example uses XML version 1.0 with UTF-8 encoding, an enumerated list of the standards used in this record with the URLs, the OBJID for this digital object represented by the METS document in the form of a URN, and a human-readable LABEL describing the work being encoded (in this case, the title of the work).

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mets:mets xmlns:mets="http://www.loc.gov/METS/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      http://www.loc.gov/standards/mets/mets.xsd"
    OBJID="ark:/13030/kt9s2009hz"
    LABEL="Martial Epigrams">
```
