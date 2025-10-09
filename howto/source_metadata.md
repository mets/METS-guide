---
title: Describing characteristics of the source material
parent: METS How-Tos
---
# Describing characteristics of the source material

**Source metadata** is descriptive and administrative metadata about the source format or media of a component of the METS object such as a digital content file. It is often used for discovery, data administration or preservation of the digital object. Source metadata can be expressed according to current source description standards (such as PREMIS) or a locally produced XML schema.

For our *Epigrams* example digital object, we could have used `<md>` to link to the MARC record describing the print version of the book from which the images were derived. As another example, when a digital audio object is created from an open reel tape, we can record important technical metadata about the tape in a `<md>` element with a `USE="SOURCE"` attribute, within an `<mdWrap>` element, as follows:

## TODO use current version of AES schema

```xml
<mets:md ID="SMD_MJF_Tape_0010_Side_A" STATUS="Draft, unformatted"
    CREATED="2006-08-28T15:36:53" USE="SOURCE">
  <mets:mdWrap MDTYPE="Draft AES-X098-SC-03-06-B, version 2006-05-19"
      MIMETYPE="audio/x-wave">
    <mets:xmlData>
      <dataroot xmlns:od="urn:schemas-microsoft-com:officedata"
          generated="2006-08-28T15:36:53">
        <source>
          <ID>1</ID>
          <source_metadata_id>SRC000000001</source_metadata_id>
          <item_face_id_fk>IF000000001</item_face_id_fk>
          <identifier>0001</identifier>
          <identifier_type>MJF tape number</identifier_type>
          <direction>A_PASS</direction>
          <source_format_type>open reel tape</source_format_type>
          <analog_digital_flag>analog</analog_digital_flag>
          <speed>7.5</speed>
          <speed_unit>Inches per second</speed_unit>
          <track_format>half track</track_format>
          <sound_field>stereo</sound_field>
          <noise_reduction>none</noise_reduction>
          <equalization>none</equalization>
          <gauge>0.25</gauge>
          <gauge_unit>Inches</gauge_unit>
          <reel_diameter>7</reel_diameter>
          <reel_diameter_unit>Inches</reel_diameter_unit>
          <bit_depth/>
          <sample_rate/>
        </source>
      </dataroot>
    </mets:xmlData>
  </mets:mdWrap>
</mets:md>
```
