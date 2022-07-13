
All significant changes to this FHIR implementation guide will be documented on this page.

### v0.4.0 (from July 2022)

#### Open Issues
* ...

See also open issues on [GitHub](https://github.com/ahdis/hci-analyzer/issues).

#### Added
* Add slices for different entries in the Bundle to simplify the validation.

#### Changed / Updated
* The working hypothesis until v0.3.0 was that the Medication List document as a dynamically generated document will not appear as an input document for the analyzer. This hypothesis was disproved and the implementation guide adapted accordingly (graphics, use case, examples, profiles). 
* Profiles Output Document: Remove the minimum cardinality from following elements (for author medical decision) for the case, that the Composition.author from the Input Document is a Device
   * [Analyzer MedicationStatement Header](StructureDefinition-analyzer-medicationstatement-header.html):  informationSource -> Reference(Analyzer Patient \| Analyzer Practitioner)
   * [Analyzer MedicationStatement](StructureDefinition-analyzer-medicationstatement.html): informationSource	-> Reference(Analyzer Patient \| Analyzer Practitioner)
   * [Analyzer MedicationRequest](StructureDefinition-analyzer-medicationrequest.html):  performer -> Reference(Analyzer Practitioner)
   * [Analyzer MedicationDispense](StructureDefinition-analyzer-medicationdispense.html): performer.actor -> Reference(Analyzer Practitioner)
   * [Analyzer Observation PADV](StructureDefinition-analyzer-observationpadv.html): performer -> Reference(Analyzer Practitioner)

#### Fixed




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
* Initial version of this implementation guide on which the 'Documedis Medical Data Analyzer CE (v1.0.0.0)' as a certified medical device is based.   
* Based on CH EMED (v0.1.0) and CHMED (v1.0.0).
* This version was not published. The status at that time corresponds to this CHMED [commit](https://github.com/ahdis/chmed/tree/371f5c04ecca44f0860047ebbc1a25ca60987ae4) from May 2020.
