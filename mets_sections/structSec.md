---
title: Structure section
parent: Sections of a METS Document
nav_order: 5
---
# Structure section

The **structure section** `<structSec>` provides a means of organizing the digital content represented by the `<file>` elements in the `<fileSec>` of the METS document into a coherent hierarchical structure. (Note that if there is another structure that better suits your needs, that is fine, but hierarchical structures are most commonly used here.) Such a hierarchical structure can be presented to users to help them understand and navigate the digital content. It can also be used for any purpose that requires an understanding of the structural relationship of content files or parts of content files. The organization can be specified at any desired level of granularity (intellectual and/or physical). The section may contain one or more structural maps, using a repeatable `<structMap>` element that allows more than one structure to apply to the digital content represented by the METS document.

The structure provided by the `<structMap>` element may be purely intellectual or logical (such as a book divided into chapters), purely physical (a book divided into sequences of pages), or a mixture of logical and physical (a book divided into chapters and then into a sequence of pages). The content organized by the `<structMap>` can include many mixtures of digital content files: structured or unstructured text, image, audio, video, and/or application (such as PDF).

In addition to the content represented by the files in the `<fileSec>` of the same METS documents, a `<structMap>` can also encompass and organize content represented by integral, external METS documents. For example, the `<structMap>` of a METS document representing a digital version of a journal series might organize the multiple external METS documents representing each issue of the journal in order of publication. The `<structMap>` elements of the METS documents representing the individual issues could then organize their contents.

In addition to providing a means for organizing content, the `<structMap>` also provides a mechanism for linking content at any hierarchical level with relevant metadata. For more on this type of linking, see "[Representing parts of a digital object](../howto/div.md)".

The hierarchical structure specified by a `<structMap>` is encoded as a tree of nested `<div>` elements. A `<div>` element may point directly to content via child file pointer (`<fptr>`) elements (if the content is represented in the `<fileSec>`) or via child METS pointer (`<mptr>`) elements (if the content is represented by an external METS document). The `<fptr>` element may point to a single `<file>` element that manifests its parent `<div>`, or point to part of a `<file>` that manifests its `<div>`. It can also point to multiple files or parts of files, which must be played or displayed either in sequence or in parallel to render the structural division. The `<div>`, `<mptr>`, `<fptr>`, and other `<structMap>` elements that enable this sophisticated structuring are described in detail on their own pages (see [Structuring and Linking](../mets_howtos.md#structuring-and-linking))

The example encodings in this structure section demonstrate a variety of ways to structure a digital version of the Martial *Epigrams*, some more plausible than others. The main goal is not to present definitive encodings, but rather just to showcase the flexibility and variety of the structural mechanisms offered by METS. The best structural choices for a particular work depend on several factors: the nature of the work being digitized, the anticipated users of the digital version, the type(s) of presentation desired, the capabilities of the available presentation tools, etc.

## More Information

* [Representing parts of a digital object](../howto/div.md)
* [Connecting structure and content with file pointers](../howto/fptr.md)
* [Composing digital objects from multiple METS documents with METS pointers](../howto/mptr.md)
* [Including parts of files in the structure](../howto/area.md)
* [Presenting content sequentially](../howto/seq.md)
* [Presenting content simultaneously (in parallel)](../howto/par.md)
