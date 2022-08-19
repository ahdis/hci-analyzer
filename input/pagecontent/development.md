### Output Document - Consolidated Medication Card document

#### Header MedicationStatement
* There must be at least one dosage element. If there is no dosage information, this element `"text" : "-"` is listed.

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

