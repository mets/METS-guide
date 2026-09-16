---
title: Including parts of files in the structure
parent: METS How-Tos
---
# Including parts of files in the structure

The **area** `<area>` element typically points to content consisting of just a portion or area of a file represented by a `<file>` element in the `<fileSec>` In some contexts, however, the `<area>` element can also point to content represented by an integral file.

A single `<area>` element would appear as the direct child of a `<fptr>` element when only a portion of a `<file>`, rather than an integral `<file>`, manifested the digital content represented by the `<fptr>` In this case the `<area>` element both identifies the pertinent `<file>` via its FILEID attribute and specifies the pertinent area of that file via its SHAPE and COORDS attributes (in the case of image content) or some combination of BETYPE, BEGIN, END, EXTTYPE and EXTENT attributes (in the case of text or audio /video content).

Multiple `<area>` elements would appear as the direct children of a `<par>` element or a `<seq>` element when multiple files or parts of files manifested the digital content represented by an `<fptr>` element; see also "[Presenting content sequentially](seq.md)" and "[Presenting content simultaneously (in parallel)](par.md)".  As described there, the `<par>` and `<seq>` elements are used to group multiple files or parts of files that must be played/displayed in parallel or in sequence to manifest the digital content represented by the parent `<fptr>` element. In these cases, each individual file, or file segment, would be represented by a child `<area>` element. When used as the direct child of an `<fptr>` element, as is described in the paragraph above, the `<area>` element typically points to just an area or segment of an integral file. When used in the context of a `<par>` or `<seq>` element, however, an area element can point either to an integral file or to a segment of a file as necessary.

## Example

The example below demonstrates the use of the `<area>` element to isolate particular areas of the image files that are referenced in the associated FILEID attributes. It shows both uses of the `<area>` element as a direct child of an `<fptr>` element and as a direct child of a `<seq>` element. In the former case, the specified area of the referenced image manifests the parent division by itself. In the latter case, the specified areas of two different images must be displayed in sequence to fully manifest the parent division.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mets:mets xmlns:mets="http://www.loc.gov/METS/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      http://www.loc.gov/standards/mets/mets.xsd"
    OBJID="ark:/13030/kt9s2009hz" LABEL="Martial Epigrams">
  <mets:fileSec>
    <mets:fileGrp USE="REFERENCE IMAGE">
      <mets:file ID="epi09r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpg/09.jpg"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi11r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpg/11.jpg"
          LOCTYPE="URL"/>
      </mets:file>
      <mets:file ID="epi13r" MIMETYPE="image/jpeg">
        <mets:FLocat LOCREF="http://www.loc.gov/standards/mets/docgroup/jpeg/13.jpg"
          LOCTYPE="URL"/>
      </mets:file>
    </mets:fileGrp>
  </mets:fileSec>
  <mets:structSec>
    <mets:structMap TYPE="logical">
      <mets:div TYPE="volume" LABEL="Martial Epigrams II">
        <mets:div TYPE="section" LABEL="Book VIII">
          <mets:div TYPE="introduction" LABEL="Introduction: Latin">
            <mets:fptr>
              <mets:seq>
                <mets:area FILEID="epi09r" SHAPE="RECT" COORDS="0,1150,2500,3150"/>
                <mets:area FILEID="epi11r" SHAPE="RECT" COORDS="0,600,2500,900"/>
              </mets:seq>
            </mets:fptr>
          </mets:div>
          <mets:div TYPE="epigram" LABEL="Epigram I: Latin">
            <mets:fptr>
              <mets:area FILEID="epi11r" SHAPE="RECT" COORDS="0,1000,2500,1500"/>
            </mets:fptr>
          </mets:div>
          <mets:div TYPE="epigram" LABEL="Epigram II: Latin">
            <mets:fptr>
              <mets:area FILEID="epi11r" SHAPE="RECT" COORDS="0,1500,2500,2350"/>
            </mets:fptr>
          </mets:div>
          <mets:div TYPE="epigram" LABEL="Epigram III: Latin">
            <mets:fptr>
              <mets:seq>
                <mets:area FILEID="epi11r" SHAPE="RECT" COORDS="0,2350,2500,3050"/>
                <mets:area FILEID="epi13r" SHAPE="RECT" COORDS="0,500,2500,2100"/>
              </mets:seq>
            </mets:fptr>
          </mets:div>
          <mets:div TYPE="epigram" LABEL="Epigram IV: Latin">
            <mets:fptr>
              <mets:area FILEID="epi13r" SHAPE="RECT" COORDS="0,2100,2500,2700"/>
            </mets:fptr>
          </mets:div>
        </mets:div>
      </mets:div>
    </mets:structMap>
  <mets:structSec>
</mets:mets>
```

For further examples of how the `<area>` element can be used in the context of the `<seq>` and `<par>` elements, see also:

* [Presenting content sequentially](seq.md)
* [Presenting content simultaneously (in parallel)](par.md)
