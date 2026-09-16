---
title: Connecting structure and content with file pointers
parent: METS How-Tos
---
# Connecting structure and content with file pointers

The `<fptr>` or **file pointer** element represents digital content that manifests its parent `<div>` element. The content represented by an `<fptr>` element must consist of integral files or parts of files that are represented by `<file>` elements in the `<fileSec>` Via its FILEID attribute, an `<fptr>` may point directly to a single integral `<file>` element that manifests a structural division. (See also "[Referring to elements within METS](idrefs_within_mets.md)").  However, an `<fptr>` element may also govern an `<area>` element, a `<par>` element, or a `<seq>` element which in turn would point to the relevant file or files. A child `<area>` element can point to part of a `<file>` that manifests a division, while the `<par>` and `<seq>` elements can point to multiple files or parts of files that together manifest a division. (For fuller information on the `<area>`, `<par>`, and `<seq>` elements see also "[Including parts of files in the structure](area.md)", "[Presenting content sequentially](seq.md)", and [Presenting content simultaneously (in parallel)](par.md).

More than one `<fptr>` element can be associated with a `<div>` element.  Typically sibling `<fptr>` elements represent alternative versions, or manifestations, of the same content. For example, a page of a manuscript might be represented by a thumbnail image, a reference image, a master image, and a structured text version of the page content. Each of these versions would be represented by a `<file>` element in the `<fileSec>` The `<div>` element in the `<structMap>` corresponding to this page of the manuscript would therefore have four child `<fptr>` elements, each of which points to one of the alternative versions of the content.  Typically sibling `<fptr>` elements represent alternative versions, or manifestations, of the same content. Additional attributes associated with the `<fptr>` element include ID and CONTENTIDS. Descriptions of all of the attributes associated with the `<fptr>` element appear in the [schema documentation](https://mets.github.io/METS_v2_Docs/mets2_xsd.html#divType_fptr).

## Example

The following METS encoding fragment represents a case where the `<structMap>` as a whole represents a purely physical structure. The root division represents the whole book, and each structural division under this root represents a physical page. Each page division has three associated content files, each of which represents a different image manifestation (TIFF, JPEG, or GIF) of the same content:

```xml
<mets:mets xmlns:mets="http://www.loc.gov/METS/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      http://www.loc.gov/standards/mets/mets.xsd"
    OBJID="ark:/13030/kt9s2009hz" LABEL="Martial Epigrams II">
  [...]
  <mets:fileSec>
    <mets:fileGrp USE="MASTER IMAGE">
      <mets:file ID="epi01m" MIMETYPE="image/tiff">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/full01.tif"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi02m" MIMETYPE="image/tiff">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/full/02.tif"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi03m" MIMETYPE="image/tiff">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/full/03.tif"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi04m" MIMETYPE="image/tiff">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/full/04.tif"
          LOCTYPE="URL"/>
      </mets:file>
      [...]
    </mets:fileGrp>
    <mets:fileGrp USE="REFERENCE IMAGE">
      <mets:file ID="epi01r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpg/01.jpg"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi02r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpg/02.jpg"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi03r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpg/03.jpg"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi04r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpg/04.jpg"
          LOCTYPE="URL"/>
      </mets:file>
      [...]
    </mets:fileGrp>
    <mets:fileGrp USE="THUMBNAIL IMAGE">
      <mets:file ID="epi01t" MIMETYPE="image/gif">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/gif/01.gif"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi02t" MIMETYPE="image/gif">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/gif/02.gif"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi03t" MIMETYPE="image/gif">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/gif/03.gif"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi04t" MIMETYPE="image/gif">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/gif/04.gif"
          LOCTYPE="URL"/>
      </mets:file>
      [...]
    </mets:fileGrp>
  </mets:fileSec>
  <mets:structSec>
    <mets:structMap TYPE="physical">
      <mets:div TYPE="book" LABEL="Martial Epigrams II" MDID="DMD1">
        <mets:div TYPE="page" LABEL="Blank page">
          <mets:fptr FILEID="epi01m"/>
          <mets:fptr FILEID="epi01r"/>
          <mets:fptr FILEID="epi01t"/>
        </mets:div>
        <mets:div TYPE="page" LABEL="Page i: Half title page">
          <mets:fptr FILEID="epi02m"/>
          <mets:fptr FILEID="epi02r"/>
          <mets:fptr FILEID="epi02t"/>
        </mets:div>
        <mets:div TYPE="page" LABEL="Page ii: Blank page">
          <mets:fptr FILEID="epi03m"/>
          <mets:fptr FILEID="epi03r"/>
          <mets:fptr FILEID="epi03t"/>
        </mets:div>
        <mets:div TYPE="page" LABEL="Page iii: Title page">
          <mets:fptr FILEID="epi04m"/>
          <mets:fptr FILEID="epi04r"/>
          <mets:fptr FILEID="epi04t"/>
        </mets:div>
        ...
      </mets:div>
    </mets:structMap>
  <mets:structSec>
</mets:mets>
```
