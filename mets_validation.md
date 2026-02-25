---
title: Validating METS documents
nav_order: 8
---

# Validating METS documents

METS documents are created following the ruleset described in the METS XML-schema that specifies all the elements and attributes that can be used.  In addition to these elements and attributes, the schema also contains the requirements regarding the structure and supported values. for the defined elements and attributes. This is described for METS version 1 in the Primer and for METS version 2 in the METS Guide.

To observe is that there is a possibility in some elements to add your own attributes, the own attributes are not part of the METS XML-schema. This setup is not depending on the version of METS.

## Best practices in Digital Preservation

When using METS, a good practice is to make sure that you always are validating your XML-documents no matter what type of standard that is being used. While the schemas are generally available at the standards’ hosting institution, it is recommended to locally store the XML-schemas and validation rules. This is a best practice based on the need for keeping the XML-schemas and the versions of them used in the different XML-documents available throughout the whole lifecycle of the XML-documents and making sure that you are using the correct version of the XML-schema to validate your XML-document. You also need to have in mind that there are occasions when the original source for the XML-schema might not be available either because your repository is sealed off from the internet environment or the original source for some reason not being available on the internet. To further enhance the practice a good plan is to make sure that all the used XML-schemas are part of the digital package to make sure that you always have access to the correct version of rulesets.

### METS Profiles and METS XML-schema

The METS profiles that are created describing the local use of METS are not directly connected to the METS XML-schema and cannot be used to formally validate METS documents. This means that other ways of expressing the local use and its rules needs to be used to facilitate validation.

### Expressing local METS rules with Schematron

The local rules are easiest captured through the use of Schematron. Schematron is an ISO standard that describes how to create validation rulesets for XML-documents without making adaptations to an XML-schema and by this keeping the XML-schema in its original state. With Schematron, you can also cover more aspects to verify than with an XML schema.

#### Introduction to Schematron

XML-schema (and RNG-schema) have limitations in which types of validations it is possible to carry out. For example it is not possible to do conditional validation using just the XML schema language. To overcome this Schematron was developed. Schematron is an ISO standard where more information is available here: http://schematron.com/. If you are new to Schematron this is a good resource: http://www.mulberrytech.com/papers/schematron-Philly.pdf 

#### METS and Schematron

METS in both versions are based on using Schematron for aiding with validation and not making any adaptations in the XML-schema. When using METS the best option is to have the schema saved locally and with it you need to place your Schematron validation rules. The Schematron document is used for validations of for example an obligation that has been locally defined for the number of files that needs to be described in a METS-document. All the local rules are needed to be put in a Schematron document. It is possible to write both simple and complicated validation scenarios using Schematron. You need to investigate what you need.

#### Schematron and XML validation

Due to the extension of the validation with Schematron you need to make sure that the validation takes place. Not all validators manage to do this automatically, you may need to do some settings but it all depends on the validator.
At the same time, it differs with how the Schematron rules are called by the XML-document. If you are using the XML-schema it is not possible to call the Schematron rules within the schema. Instead, the validator and/or the XML-document needs to have the setting for using the Schematron document. How to do it depends on the validator you are using and you need to investigate and implement the correct way for your validator.

#### Your own Schematron rules

You put your rules in its own Schematron document which with the added line <extends href="Name of Schematron document.sch"/> calls the Schematron documents which are being extended if that is occurring. Replace “Name of Schematron document” with the name of the Schematron document.

#### An example

This is an example of the extension Schematron document with the extra rules I have specified for my METS documents. The rule I have is that there needs to be files described in the METS-document.

There are two different URI:s used, one for METS version 1 and One for METS version 2. They are both given here:
URI METS 1: Add URI
URI METS 2: Add URI

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://purl.oclc.org/dsdl/schematron"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform" queryBinding="xslt2">
 <ns uri="the uri for the version of METS that is going to be validated" prefix="mets"/>
    
    <extends href="mets.sch"/> <!-- to be used if we have a base METS schematron document for validation! -->
    
    <!-- Here follow all the rules for the local adaption of METS -->
    <pattern id="count number of file groups">
        <rule context="mets:fileSec">
            <!-- In the mets element we check that the element fileSec is present -->
            <!-- First an assert test so the element fileSec is present. If its not present its an error -->
            <!-- Second a report test to see if the element fileGrp is present. This is just information -->
            <assert test="exists(fileSec)">Error message, the element fileSec must be present in the METs document</assert>
            <report test="exists(fileGrp)">Contol message, the element fileGrp is present in the fileSec element</report>
        </rule>
    </pattern>
</schema>
```
