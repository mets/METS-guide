---
title: Referring to elements within METS
parent: METS How-Tos
---
# Referring to elements within METS

METS makes extensive provisions for using the [ID, IDREF, and IDREFS attributes](id_idrefs.md) to create cross-references between related elements. Ultimately, these provisions allow units of information appearing in dispersed locations across a METS instance document to be linked to all of their appropriate contexts without redundancy. METS `<md>` and `<file>` elements have required ID attributes, which allow the metadata and content file elements to be referenced from the other parts of the METS instance document to which they pertain. In addition, ``<div>`` elements in the ``<structMap>`` and many other elements can include ID attribute values that allow them to be referenced by other elements. METS’ specific cross-referencing provisions for different contexts are outlined below.

## Context 1: `<md>` metadata

* A unique ID attribute value must identify each `<md>` element in a METS instance document.
* Each of the following elements can reference one or more specific `<md>` elements by citing their ID values in their MDID attribute (the MDID attribute is of type IDREFS):
  * mets/metsHdr
  * mets/mdSec/md
  * mets/fileSec/fileGrp
  * mets/fileSec/fileGrp/file
  * mets/fileSec/fileGrp/file/stream 
  * mets/structMap/div
  * mets/structMap/div/fptr//area

### Example 1: Descriptive metadata

In the example below the ID attribute value of “MD1” identifies the single `<md>` element. The root `<div>` in the `<structMap>` references this `<md>` element by means of its MDID attribute. Thus, the encoding indicates that the descriptive metadata in the `<md>` element identified by the ID value “MD1” applies to the entire content as represented by the root `<div>` in the `<structMap>`.
```xml
<mets:mets
    xmlns:mets="http://www.loc.gov/METS/v2"
    xmlns:mods="http://www.loc.gov/mods/v3"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      https://github.com/mets/METS-schema/raw/mets2/v2/mets.xsd
      http://www.loc.gov/mods/v3 http://www.loc.gov/mods/v3/mods-3-1.xsd"
    OBJID="ark:/13030/kt9s2009hz" LABEL="Martial Epigrams">
  <mets:mdSec>
    <mets:md ID="MD1">
      <mets:mdWrap MDTYPE="MODS">
        <mets:xmlData>
          <mods:mods>
            <mods:titleInfo>
              <mods:title>Martial Epigrams</mods:title>
            </mods:titleInfo>
          </mods:mods>
        </mets:xmlData>
      </mets:mdWrap>
    </mets:md>
  </mets:mdSec>
  <mets:structSec>
    <mets:structMap TYPE="physical">
      <mets:div TYPE="book" LABEL="Martial Epigrams II" MDID="MD1"/>
    </mets:structMap>
  </mets:structSec>
</mets:mets>
```
### Example 2: Administrative metadata

In the example below, the ID attribute value “App4ADM1” identifies the first `<md>` element, and the value “App4ADM2” identifies the second `<md>` element. The MDID attribute on the single `<file>` element in the `<fileSec>` references both of these ID values (“App4ADM1 App4ADM2”). Thus, the encoding indicates that both the technical metadata in the first `<md>` element (“App4ADM1”) and the rights metadata in the second `<md>` element (“App4ADM2”) apply to the content file represented by the `<file>` element.

```xml
<mets:mets
    xmlns:mets="http://www.loc.gov/METS/v2"
    xmlns:mods="http://www.loc.gov/mods/v3"
    xmlns:rts="http://cosimo.stanford.edu/sdr/metsrights/"
    xmlns:mix="http://www.loc.gov/mix/v20"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.loc.gov/METS/v2
      https://github.com/mets/METS-schema/raw/mets2/v2/mets.xsd 
      http://cosimo.stanford.edu/sdr/metsrights/
      https://www.loc.gov/standards/rights/METSRights.xsd
      http://www.loc.gov/mods/v3
      http://www.loc.gov/standards/mods/v3/mods-3-1.xsd
      http://www.loc.gov/mix/v20
      http://www.loc.gov/standards/mix/mix.xsd"
    OBJID="ark:/13030/hb3c6005tv" TYPE="still image"
    LABEL="S. P. [Simmon Peña] Storms, Interpreter [&amp;c], Indian agency - near Grass Valley, California, 1851"
    PROFILE="http://www.loc.gov/standards/mets/profiles/0000000X.xml">
  <mets:mdSec>
    <mets:md ID="App4ADM1">
      <mets:mdWrap MDTYPE="MIX">
        <mets:xmlData>
          <mix:mix>
            <mix:BasicImageParameters>
              <mix:Format>
                <mix:MIMEType>image/tiff</mix:MIMEType>
                <mix:Compression>
                  <mix:CompressionScheme>1</mix:CompressionScheme>
                </mix:Compression>
                <mix:PhotometricInterpretation>
                  <mix:ColorSpace>2</mix:ColorSpace>
                  <mix:ICCProfile>
                    <mix:ProfileName>DilE836G18_01</mix:ProfileName>
                  </mix:ICCProfile>
                </mix:PhotometricInterpretation>
              </mix:Format>
            </mix:BasicImageParameters>
            <mix:ImageCreation>
              <mix:ImageProducer>DIL/U.C. Berkeley Library</mix:ImageProducer>
              <mix:DeviceSource>reflection print scanner</mix:DeviceSource>
              <mix:ScanningSystemCapture>
                <mix:ScanningSystemHardware>
                  <mix:ScannerManufacturer>Epson</mix:ScannerManufacturer>
                  <mix:ScannerModel>
                    <mix:ScannerModelName>836xl</mix:ScannerModelName>
                    <mix:ScannerModelSerialNo>B05401003MG9601009</mix:ScannerModelSerialNo>
                  </mix:ScannerModel>
                </mix:ScanningSystemHardware>
              </mix:ScanningSystemCapture>
            </mix:ImageCreation>
            <mix:ImagingPerformanceAssessment>
              <mix:SpatialMetrics>
                <mix:SamplingFrequencyUnit>2</mix:SamplingFrequencyUnit>
                <mix:XSamplingFrequency>600</mix:XSamplingFrequency>
                <mix:YSamplingFrequency>600</mix:YSamplingFrequency>
              </mix:SpatialMetrics>
              <mix:Energetics>
                <mix:BitsPerSample>8,8,8</mix:BitsPerSample>
                <mix:SamplesPerPixel>3</mix:SamplesPerPixel>
              </mix:Energetics>
            </mix:ImagingPerformanceAssessment>
          </mix:mix>
        </mets:xmlData>
      </mets:mdWrap>
    </mets:md>
    <mets:md ID="App4ADM2">
      <mets:mdWrap MDTYPE="METSRights">
        <mets:xmlData>
          <rts:RightsDeclarationMD RIGHTSCATEGORY="OTHER" OTHERCATEGORYTYPE="UNKNOWN">
            <rts:RightsHolder>
              <rts:RightsHolderComments>All requests to reproduce, publish,
                quote from, or otherwise use collection materials must be
                submitted in writing to the Head of Access Services,
                The Bancroft Library, University of California, Berkeley
                94720-6000. Consent is given on behalf of The Bancroft
                Library as the owner of the physical items and does not
                constitute permission from the copyright owner. Such
                permission must be obtained from the copyright owner.
                See: http:// bancroft.berkeley.edu/reference/permissions.html
              </rts:RightsHolderComments>
            </rts:RightsHolder>
            <rts:Context CONTEXTCLASS="GENERAL PUBLIC">
              <rts:Constraints>
                <rts:ConstraintDescription>Copyright status unknown. Some
                  materials in these collections may be protected by the U.S.
                  Copyright Law (Title 17, U.X.C.). In addition, the
                  reproduction of some materials may be restricted by terms of
                  University of California gift or purchase agreements, donor
                  restrictions, privacy and publicity rights, licensing and
                  trademarks. Transmission or reproduction of materials
                  protected by copyright beyond that allowed by fair use
                  requires the written permission of copyright owners. Works
                  not in the public domain cannot be commercially exploited
                  without permission of the copyright owner. Responsibility for
                  any use rests exclusively with the user.
                </rts:ConstraintDescription>
              </rts:Constraints>
            </rts:Context>
          </rts:RightsDeclarationMD>
        </mets:xmlData>
      </mets:mdWrap>
    </mets:md>
  </mets:mdSec>
  <mets:fileSec>
    <mets:fileGrp VERSDATE="2003-01-22T00:00:00.0" USE="archive image">
      <mets:file ID="App4FID1" MIMETYPE="image/tiff" SEQ="1"
          CREATED="2003-01-22T00:00:00.0" MDID="App4ADM1 App4ADM2" GROUPID="GID1">
        <mets:FLocat LOCTYPE="URL"
          LOCREF="http://offlineimage/calcultures/ucb/cubanc_1_2_00004722a.tif"/>
      </mets:file>
    </mets:fileGrp>
  </mets:fileSec>
  <mets:structSec>
    <mets:structMap TYPE="physical">
      <mets:div ORDER="1" TYPE="still image"
          LABEL="S. P. [Simmon Peña] Storms, Interpreter [&#x26;c],
            Indian agency - near Grass Valley, California, 1851">
        <mets:fptr FILEID="App4FID1"/>
      </mets:div>
    </mets:structMap>
  </mets:structSec>
</mets:mets>
```
## Context 2: `<file>` content files

* A unique ID attribute value must identify each `<file>` element in the `<fileSec>` of a METS document.
* Each of the following elements can reference the specific `<file>` pertinent to it by citing the `<file>` element’s ID value in its FILEID attribute (the FILEID attribute is of type IDREF).
  * mets/structMap/div/fptr
  * mets/structMap/div/fptr/area
  * mets/structMap/div/fptr/seq/area
  * mets/structMap/div/fptr/par/area
  * mets/structMap/div/fptr/par/seq/area
### Example
Example 2 from the previous context also demonstrates this one. In that example, the ID attribute value “App4FID1” identifies the single `<file>` element. The single `<fptr>` element under the root `<div>` of the `<structMap>` references this ID value. Thus, the encoding indicates that the content file represented by the `<file>` element with the ID value “App4FID1” manifests the root `<div>` element.
