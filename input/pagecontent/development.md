### Output Document - Consolidated Medication Card document

#### Header MedicationStatement
##### Dosage
* There must be at least **one dosage element** (non-structrued/structured-normal/structured-split).
* The dosage element (1..*) is set according to this scheme:
   1. The dosage element is taken from the **last CHANGE** (Observation.code = CHANGE, see also [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html))
   2. If there is **no** CHANGE (see decision 1), the dosage element is taken from the **newest resource** (MedicationStatement/MedicationDispense/MedicationRequest)
   3. If the last resource is an **Observation (PADV)**, then it depends on the Observation.code (see also [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html)):   
      a. **OK**: decision 1/2   
      b. **CHANGE**: decision 1   
      c. **CANCEL**: dosage with this element `"text" : "-"` is listed   
      d. **COMMENT**:  decision 1/2   

#### Authors
##### Author of the document
* The author of the document in the output documet is always the Analyzer as device:   
   * Composition.author -> Reference(Analyzer Device) ([profile](StructureDefinition-analyzer-out-composition.html))

##### Author of the medical decision
* The author of the medical decision in the output document is mapped in these elements:
   * Header MedicationStatement.informationSource ([profile](StructureDefinition-analyzer-medicationstatement-header.html))
   * MedicationStatement.informationSource ([profile](StructureDefinition-analyzer-medicationstatement.html))
   * MedicationDispense.performer.actor ([profile](StructureDefinition-analyzer-medicationdispense.html))
   * MedicationRequest.performer ([profile](StructureDefinition-analyzer-medicationrequest.html))
   * Observation.performer ([profile](StructureDefinition-analyzer-observationpadv.html))

In order to map the author of the medical decision, the following procedure is followed to get the information from the input document(s):
   1. MedicationStatement.informationSource   
      -> PractitionerRole (PractitionerRole.practitioner -> Practitioner) => both resources can be taken from the input
   2. Composition.section.author   
      -> PractitionerRole (PractitionerRole.practitioner -> Practitioner) => both resources can be taken from the input
   3. Composition.author   
      -> PractitionerRole (PractitionerRole.practitioner -> Practitioner) => both resources can be taken from the input   
      -> Practitioner => generate a PractitionerRole resource with the element PractitionerRole.practitioner -> Practitioner; the Practitioner resource can then be taken from the input   
      -> Patient => the resource can be taken from the input   

#### History Changes
Codes to show the different type of changes in the medication history:
* [CodeSystem](CodeSystem-history-changes.html) & [ValueSet](ValueSet-history-changes.html)
* [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html) to show the mapping to the different types/codes of the PADV Observations (input document).