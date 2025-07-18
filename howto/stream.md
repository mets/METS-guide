---
title: Representing parts of files
parent: METS How-Tos
---
# Representing parts of files

A **component byte stream** element `<stream>` may be composed of one or more subsidiary streams. An MPEG4 file, for example, might contain separate audio and video streams, each of which is associated with technical metadata. The repeatable `<stream>` element provides a mechanism to record the existence of separate data streams within a particular file, and the opportunity to associate metadata elements `<md>` with those subsidiary data streams if desired.

When a file contains other files, such as with container file formats like `.zip`,  using child `<file>` elements is preferred (see also [Handling 'wrapper' file formats](transformFile.md)). Use `<stream>` when the subsidiary streams are logically separate entities but not individual files in their own right. 

## Example

The following simplified example is a Matroska video container file, which contains one FFV1 video stream and one FLAC audio stream.

The MDID attribute in `<file>` element refers to a metadata section which contains metadata about the file itself, where as the `MDID` attributes in the streams refer to the metadata sections, which contain metadata about the video and audio streams. These sections could for example include all the required technical metadata about the file and its streams.

```xml
<mets:fileSec>
  <mets:fileGrp>
    <mets:file MDID="tech-container" ID="id-movie" MIMETYPE="video/x-matroska">
      <mets:FLocat LOCTYPE="URL" LOCREF="file://movie.mkv" />
      <mets:stream MDID="tech-video" streamType="video/x-ffv" />
      <mets:stream MDID="tech-audio" streamType="audio/flac" />
    </mets:file>
  </mets:fileGrp>
</mets:fileSec>
```
