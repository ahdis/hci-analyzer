
All significant changes to this FHIR implementation guide will be documented on this page.

### v0.5.0 (from Jan 2023)

#### Open Issues
* 

See also open issues on [GitHub](https://github.com/ahdis/hci-analyzer/issues).

#### Changed / Updated
* Changes due to the new [CH EMED v3.0.0](https://fhir.ch/ig/ch-emed/3.0.0/index.html) and [current (CI build)](https://build.fhir.org/ig/hl7ch/ch-emed/index.html) specification
   * Input Documents:
      * Updated the CH EMED example documents
   * Output Documents: 
      * Composition.author: Changed from seperate elements 'Practitioner' and 'Organization' to 'PractitionerRole' with the respective references from there (added slice for Organization to Bundle profiles)
      * New structure of dosage element(s)
      * Change status of Header MedicationStatement to `unknown` (incl. profile)
      * Adapt the display values
      * Author of the medical decision (MedicationRequest) (see [development notes](development.html#author-of-the-medical-decision))
         * Map to MedicationRequest.requester (instead of MedicationRequest.performer) in the output document
         * Take it from MedicationRequest.requester (instead of MedicationRequest.performer) from the input document
* Rename 'Extension Input Document Type': http://hcisolutions.ch/ig/analyzer/StructureDefinition/parentdocumentid


### v0.4.0 (from July 2022 until Dec 2022)

#### Added
* Add slices for different entries in the Bundle to simplify the validation.
* Add [ValueSet Document Type](ValueSet-document-type.html) incl. binding to [Extension Input Document Type](StructureDefinition-inputdocumenttype.html) to improve the validation.
* Add ATC code (element category) to MedicationDispense and MedicationRequest (analog to MedicationStatement and MedicationStatement Header).
* Include the new extension 'Input Document Id' into the existing extension [Info Input Document](StructureDefinition-infoinputdocument.html) to represent the identifier (externalDocumentId) of the input document.
* Integrate [development notes](development.html).

#### Changed / Updated
* The working hypothesis until v0.3.0 was that the Medication List document as a dynamically generated document will not appear as an input document for the analyzer. This hypothesis was disproved and the implementation guide adapted accordingly (graphics, use case, examples, profiles). 
* Update of the output document of the analyzer; the consolidated Medication Card document is a Bundle that is no longer nested in the resource Parameters.
* Use of PractitionerRole instead of Practitioner to map the author of the medical decision, see also [here](development.html#authors).
* Adapt change typ (remove 'changeROA', add 'stop'), see [CodeSystem History Changes](CodeSystem-history-changes.html) and added [ConceptMap IHE PADV to Analyzer History Changes](ConceptMap-ihe-padv-to-analyzer-history-changes.html).



### v0.3.0 (until June 2022)
* This version was not published. The status at that time corresponds to this Analyzer [commit](https://github.com/ahdis/hci-analyzer/commit/754f53612d81614c8beefd022bedffad10946222) from July 2022.
#### Added
* Add schematic illustrations for better understanding of the Analyzer process.
* Add different profiles to support the validation.
#### Changed / Updated
* Create a separate implementation guide/GitHub repository for the Analyzer. Before it was integrated in the CHMED IG as a hidden tab.
* Adjustments to the current status of CH EMED (v2.1.0 - Ballot STU 3) and CHMED (v2.1.0 - CI Build).
   * Update examples of input documents from EPD (CH EMED).
   * Update canonical URL of underlaying IG CHMED.



### v0.2.0 (2021)
* Adjustments to the current status of CH EMED (v1.0.0) and CHMED (v2.0.0).
   * Update examples of input documents from EPD (CH EMED). 
* This version was not published. The status at that time corresponds to this CHMED [commit](https://github.com/ahdis/chmed/tree/6abdc26b260d48246ddce5240606217c2766c81d) from June 2021.



### v0.1.0 (2020)
* Initial version of this implementation guide on which the 'Documedis Medical Data Analyzer CE' as a certified medical device is based.   
* Based on CH EMED (v0.1.0) and CHMED (v1.0.0).
* This version was not published. The status at that time corresponds to this CHMED [commit](https://github.com/ahdis/chmed/tree/371f5c04ecca44f0860047ebbc1a25ca60987ae4) from May 2020.
