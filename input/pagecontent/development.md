### Output Document - Consolidated Medication Card document

#### Header MedicationStatement
##### Dosage
* There must be **at least one dosage element** (non-structrued/structured-normal/structured-split).
* The dosage element (1..*) is set according to this scheme:
   1.  If the last Observation (which isn’t necessarily the last resource) is a CHANGE (= Observation.code, see also [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html)), use the dosages contained in the resource, referenced by its `"url": "id"`-extension, if it contains a dosage.
   2. If the last Observation (which isn’t necessarily the last resource) is a CANCEL, set a constant dosage with `"text" : "-"`.
   3. Take the dosage from the newest (last) resource (MedicationStatement/MedicationDispense/MedicationRequest) having a dosage.

#### Authors
##### Author of the document
* The author of the document in the output document is always the Analyzer as device:   
   * Composition.author -> Reference(Analyzer Device) ([profile](StructureDefinition-analyzer-out-composition.html))   
     (e.g. [1-1 OUT](Bundle-1-1-ConsolidatedMedicationCard.json.html): Device/Analyzer)

##### Author of the medical decision
* The author of the medical decision in the output document is mapped in these elements:
   * Header MedicationStatement.informationSource ([profile](StructureDefinition-analyzer-medicationstatement-header.html))
   * MedicationStatement.informationSource ([profile](StructureDefinition-analyzer-medicationstatement.html))
   * MedicationDispense.performer.actor ([profile](StructureDefinition-analyzer-medicationdispense.html))
   * MedicationRequest.performer ([profile](StructureDefinition-analyzer-medicationrequest.html))
   * Observation.performer ([profile](StructureDefinition-analyzer-observationpadv.html))

In order to map the author of the medical decision, the following procedure is followed to get the information from the input document(s) - take the information from where you first get it from:
   1. MedicationStatement.informationSource / MedicationDispense.performer.actor / MedicationRequest.performer / Observation.performer   
      * -> PractitionerRole (PractitionerRole.practitioner -> Practitioner) => both resources can be taken from the input   
         * [PMP1 IN](Parameters-PMP1-Input-Analyzer.json.html): urn:uuid:3656263a-8f15-4175-975a-13524d922ce4 (PractitionerRole) -> urn:uuid:f2854370-f9b0-4893-87d2-09b6098ed641 (Practitioner) =>    
           [PMP1 OUT](Bundle-PMP1-ConsolidatedMedicationCard.json.html): PractitionerRole/Hopital -> Practitioner/DocteurHopital
   2. Composition.section.author   
      * -> PractitionerRole (PractitionerRole.practitioner -> Practitioner) => both resources can be taken from the input
         * [1-1 SectionAuthor IN](Parameters-1-1-SectionAuthor-Input-Analyzer.json.html): PractitionerRole/AuthorSectionPractitionerRole -> Practitioner/AuthorSection   
           [1-1 SectionAuthor OUT](Bundle-1-1-SectionAuthor-ConsolidatedMedicationCard.json.html): PractitionerRole/AuthorSectionPractitionerRole -> Practitioner/AuthorSection        
            
   3. Composition.author   
      * -> PractitionerRole (PractitionerRole.practitioner -> Practitioner) => both resources can be taken from the input    
         * [1-1- PRAuthor IN](Parameters-1-1-PRAuthor-Input-Analyzer.json.html): PractitionerRole/Familienpraxis -> Practitioner/FamilienHausarzt =>   
           [1-1- PRAuthor OUT](Bundle-1-1-PRAuthor-ConsolidatedMedicationCard.json.html): PractitionerRole/Familienpraxis -> Practitioner/FamilienHausarzt 
      * -> Practitioner => generate a PractitionerRole resource with the element PractitionerRole.practitioner -> Practitioner; the Practitioner resource can then be taken from the input   
         * [1-1 IN](Parameters-1-1-Input-Analyzer.json.html): Practitioner/FamilienHausarzt =>   
           [1-1 OUT](Bundle-1-1-ConsolidatedMedicationCard.json.html): PractitionerRole/Hausarzt -> Practitioner/FamilienHausarzt   
      * -> Patient => the resource can be taken from the input   
         * [1-1 PatAuthor IN](Parameters-1-1-PatAuthor-Input-Analyzer.json.html): Patient/AuthorMonikaWegmueller =>   
           [1-1 PatAuthor OUT](Bundle-1-1-PatAuthor-ConsolidatedMedicationCard.json.html): Patient/AuthorMonikaWegmueller  

#### History Changes
Codes to show the different type of changes in the medication history:
* [CodeSystem](CodeSystem-history-changes.html) & [ValueSet](ValueSet-history-changes.html)
* [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html) to show the mapping to the different types/codes of the PADV Observations (input document).