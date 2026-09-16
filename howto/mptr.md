---
title: Composing digital objects from multiple METS documents with METS pointers
parent: METS How-Tos
---
# Composing digital objects from multiple METS documents with METS pointers

Like the `<fptr>` element, the **METS pointer** `<mptr>` element represents digital content that manifests its parent `<div>` element.  Unlike the `<fptr>`, which either directly or indirectly points to content represented in the `<fileSec>` of the parent METS document, the `<mptr>` element points to content represented by an external METS document. Thus, this element allows multiple discrete and separate METS documents to be organized at a higher level by a separate METS document.  For example, METS documents representing the individual issues in the series of a journal could be grouped together and organized by a higher level METS document that represents the entire journal series. Each of the `<div>` elements in the `<structMap>` of the METS document representing the journal series would point to a METS document representing an issue. It would do so via a child `<mptr>` element. Thus the `<mptr>` element gives METS users considerable flexibility in managing the depth of the `<structMap>` hierarchy of individual METS documents.

The `<mptr>` element points to an external METS document by means of an LOCREF attribute as described in "[Linking to external resources from METS](locref.md)". This is the same mechanism used for associating `<file>` elements with external content files in the [FLocat element](FLocat.md)

## Example

The example below illustrates the application of the `<mptr>` element to the case of a book issued in two volumes, each of which is represented by a discrete METS document. Using the `<mptr>` element, the METS document below binds the two separate METS documents representing the individual volumes together into a single METS document representing the entire two-volume set.

```xml 
<mets:mets xmlns:mets="http://www.loc.gov/METS/v2"
    xmlns:mods="http://www.loc.gov/mods/v3"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.loc.gov/METS/v2
      http://www.loc.gov/standards/mets/mets.xsd
      http://www.loc.gov/mods/v3
      http://www.loc.gov/mods/v3/mods-3-1.xsd"
    OBJID="ark:/13030/kt9s2009hz" LABEL="Martial Epigrams I &amp; II">
  <mets:mdSec>
    <mets:md ID="DMD1" USE="DESCRIPTIVE">
      <mets:mdWrap MDTYPE="MODS">
        <mets:xmlData>
          <mods:mods>
            <mods:titleInfo>
              <mods:title>Epigrams / Martial ; with an English translation by
                Walter C.A. Ker</mods:title>
            </mods:titleInfo>
            <mods:physicalDescription>
              <mods:extent>2 v. ; 17 cm</mods:extent>
            </mods:physicalDescription>
          </mods:mods>
        </mets:xmlData>
      </mets:mdWrap>
    </mets:md>
  </mets:mdSec>
  [...]
  <mets:structSec>
    <mets:structMap TYPE="physical">
      <mets:div TYPE="multivolume book" LABEL="Martial Epigrams I &amp; II" MDID="DMD1">
        <mets:div TYPE="volume" LABEL="Volume I">
          <mets:mptr LOCTYPE="URL"
            LOCREF="http://www.loc.gov/standards/mets/documentation MatrialEpigrams.xml"/>
        </mets:div>
        <mets:div TYPE="volume" LABEL="Volume II">
          <mets:mptr LOCTYPE="URL"
            LOCREF="http://www.loc.gov/standards/mets/documentation/MatialEpigramsII.xml"/>
        </mets:div>
      </mets:div>
    </mets:structMap>
  </mets:structSec>
</mets:mets>
```
