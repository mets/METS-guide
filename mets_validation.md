---
title: Validating METS documents
nav_order: 8
---

# Validating METS documents

METS documents are created following the ruleset described in the [METS XML schema](https://loc.gov/standards/mets/mets2.xsd) that specifies all the elements and attributes that can be used as well as their structure and supported values. This is described for METS version 1 in the [Primer](https://www.loc.gov/standards/mets/METSPrimer.pdf) and for METS version 2 in the [METS Guide](https://mets.github.io/METS-guide/).

Note: The schema allows for some elements to be extended with your own attributes which are not part of the METS XML schema.

## Best practices in digital preservation

When using METS, a best practice is to make sure that you are always validating your XML documents. While the schemas are generally available at the standards’ hosting institution, it is recommended to keep a local copy of the required XML schemas and validation rules. This recommendation is based on the need for keeping the XML schemas – and the specific versions of them used in the different XML documents – available throughout the whole lifecycle of the XML documents. There are occasions when the original source for the XML schema might not be available, either because your repository is sealed off from the internet environment, or the original source for some reason is offline/not accessible. To further enhance the practice of keeping local copies, a good plan is to include all the used XML schemas as part of the digital packages to guarantee that you always have access to the correct version of rulesets.

## METS Profiles and METS XML schema

The [METS profiles](./mets_profiles.html) are a way to describe a specific use of METS in a standardized way. However, the profiles are not directly connected to the METS XML schema and cannot be used to formally validate METS documents. This means that other ways of expressing the local use and its rules needs to be used to facilitate validation.

## Expressing local METS rules with Schematron

XML schema (and RNG-schema) are limited regarding the types of validations that are possible. For example, it is not possible to do conditional validation using just the XML schema language. To overcome this, [Schematron](http://schematron.com/) was developed, and today is an ISO standard that describes how to create validation rulesets for XML documents without making adaptations to an XML schema. If you are new to Schematron you can find a good [introduction here](http://www.mulberrytech.com/papers/schematron-Philly.pdf).

### METS and Schematron

METS in both versions is easily combined with Schematron for aiding with validation and not making any adaptations to the XML schema. Extending above best practice to keep local copies of the XML schema, you should place your Schematron validation rules next to it. With Schematron you can for example specify a local requirement for the number of files that needs to be described in a METS document, or for which type of files you would want to have a specific descriptive element. All the local rules must be put into a Schematron document. It is possible to write both simple and complicated validation scenarios using Schematron.

### Schematron and XML validation

When extending the validation with Schematron you need to make sure that the validation is applied. Not all validators manage to do this automatically, you may need to configure your process depending on the validation tool.

### Example

This is an example of the extension Schematron document with the extra rules I have specified for my METS documents. The rule I have is that there needs to be files described in the METS document.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://purl.oclc.org/dsdl/schematron"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform" queryBinding="xslt2">

    <!-- Adapt this URI if you're using METS version 1 -->
    <ns uri="http://www.loc.gov/METS/v2" prefix="mets"/>
    
    <!-- to be used if we have a base METS schematron document for validation! -->
    <extends href="mets.sch"/>
    
    <!-- In the <mets> element we check that the element fileSec is present -->
    <pattern id="count number of file groups">
        <rule context="mets:fileSec">
            <!-- First an assert test so the element fileSec is present. If its not present its an error -->
            <!-- Second a report test to see if the element fileGrp is present. This is just information -->
            <assert test="exists(fileSec)">Error: the element fileSec must be present in the METs document</assert>
            <report test="exists(fileGrp)">Info: the element fileGrp is present in the fileSec element</report>
        </rule>
    </pattern>
</schema>
```
