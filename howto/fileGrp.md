---
title: Grouping related files
parent: METS How-Tos
---
# Grouping related files

A sequence of `<fileGrp>` elements can be used to group the digital files comprising the content of a METS object, either into a flat arrangement or by type. In cases where the content files are images of different formats and resolutions, for example, one could group the image content files by format and create a separate `<fileGrp>` for each image format/resolution, such as:

-   one `<fileGrp>` for the thumbnails of the images
-   one `<fileGrp>` for the higher-resolution JPEG images
-   one `<fileGrp>` for the archival TIFF images

Meanwhile, the `<structMap>` element can be used to link together the different representations of the same intellectual content.

A `<fileGrp>` may contain zero or more `<file>` elements. A `<file>` element may contain `<FLocat>` pointers to one or more external content files via a URI (see [Referencing external files](FLocat.md)) and/or may itself contain the file content as XML or binary data using the `<FContent>` element (see [Embedding file content](FContent.md)).

A nested (hierarchical) arrangement of file groups is not allowed, since complex structures are meant to be described in the structure section `<structSec>`.

## Example

The following METS fragment represents the TIFF page images of a book:

```xml
<mets:mets xmlns:mets="http://www/loc.gov/METS/v2"
    xmlns:xsi="http://www/w3/org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      http://www.loc.gov/standards/mets/mets.xsd"
    OBJID="ark:/13010/kt9s2009hz"
    LABEL="Martial Epigrams">
  [...]
  <mets:fileSec>
    <mets:fileGrp ID="TIFF_GRP01" USE="ARCHIVAL">
      [...]
  </mets:fileSec>
  [...]
```

There may be other `<fileGrp>` elements that contain JPEG or PNG versions of the same pages.
