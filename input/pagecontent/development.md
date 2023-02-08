- [Input Document](#input-document)
  - [Input Document Source](#input-document-source)
- [Output Document - Consolidated Medication Card document](#output-document---consolidated-medication-card-document)
  - [Header MedicationStatement](#header-medicationstatement)
    - [Elements allowed](#elements-allowed)
    - [Dosage](#dosage)
  - [Id \& Identifier](#id--identifier)
  - [Status](#status)
  - [Authors](#authors)
    - [Author of the document](#author-of-the-document)
    - [Author of the medical decision](#author-of-the-medical-decision)
  - [Patient](#patient)
    - [Identifier](#identifier)
  - [Info Input Document](#info-input-document)
    - [Input Document Source](#input-document-source-1)
    - [Input Document Type](#input-document-type)
    - [Input Document Id](#input-document-id)
  - [History Changes](#history-changes)
- [FHIR Implementation Guide](#fhir-implementation-guide)
  - [Naming](#naming)

### Input Document

#### Input Document Source
See section [here](#input-document-source-1).

### Output Document - Consolidated Medication Card document

#### Header MedicationStatement

##### Elements allowed
In the [Header MedicationStatement](StructureDefinition-analyzer-medicationstatement-header.html), only the following elements are taken over or set:
* contained
* identifier (new)
* status
* category 
* medicationReference
* subject
* informationSource
* derivedFrom (set)
* dosage (taken over, see below)

##### Dosage
* There must be **at least one dosage element**.
* The dosage element (1..*) is set according to this scheme:
   1.  If the last Observation (which isn’t necessarily the last resource) is a CHANGE (= Observation.code, see also [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html)), use the dosages contained in the resource, referenced by its `"url": "id"`-extension, if it contains a dosage.
   2. If the last Observation (which isn’t necessarily the last resource) is a CANCEL, set a constant dosage with `"text" : "-"`.
   3. Take the dosage from the newest (last) resource (MedicationStatement/MedicationDispense/MedicationRequest) having a dosage.


#### Id & Identifier

{:class="table table-bordered"}
| Reource | Id | Identifier |
| --- | --- | --- |
| **MedicationStatement Header** | new | new (`urn:uuid:<id>`) |
| **Original entries (derivedFrom)**<br>(MedicationStatement/MedicationRequest/MedicationDispense/Observation) | new | remains unchanged |


#### Status

{:class="table table-bordered"}
| Reource | Status | 
| --- | --- | --- |
| **MedicationStatement Header** | new (`unknown`) |
| **Original entries (derivedFrom)**<br>(MedicationStatement/MedicationRequest/MedicationDispense/Observation) | remains unchanged |
| **Observation History** | set (`final`) |


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
      * -> PractitionerRole (PractitionerRole.practitioner -> Practitioner &#0124; PractitionerRole.organization -> Organization) => all resources can be taken from the input   
         * [PMP1 IN](Parameters-PMP1-Input-Analyzer.json.html): urn:uuid:3656263a-8f15-4175-975a-13524d922ce4 (PractitionerRole) -> urn:uuid:f2854370-f9b0-4893-87d2-09b6098ed641 (Practitioner) =>    
           [PMP1 OUT](Bundle-PMP1-ConsolidatedMedicationCard.json.html): PractitionerRole/Hopital -> Practitioner/DocteurHopital
            * see [schematic illustration](PR-UCs-PMP1.jpg)
         * PMP2: see [schematic illustration](PR-UCs-PMP2.jpg)
         * PMP3: see [schematic illustration](PR-UCs-PMP3.jpg)     
      * **Note**: If there is a changed MedicationStatement (PADV CHANGE) without informationSource, take the Observation.performer, from where the changed MedicationStatement is referenced (see PMP1 UC). 

   2. Composition.section.author   
      * -> PractitionerRole (Pracstatus value="comptitionerRole.practitioner -> Practitioner &#0124; PractitionerRole.organization -> Organization) => all resources can be taken from the input
         * [1-1 SectionAuthor IN](Parameters-1-1-SectionAuthor-Input-Analyzer.json.html): AuthorSectionPractitionerRole -> AuthorSection &#0124; AuthorSectionOrganization =>   
           [1-1 SectionAuthor OUT](Bundle-1-1-SectionAuthor-ConsolidatedMedicationCard.json.html): AuthorSectionPractitionerRole -> AuthorSection &#0124; AuthorSectionOrganization         

   3. Composition.author   
      * -> PractitionerRole (PractitionerRole.practitioner -> Practitioner &#0124; PractitionerRole.organization -> Organization) => all resources can be taken from the input    
         * [1-1 IN](Parameters-1-1-Input-Analyzer.json.html): FamilienHausarztAtHausarzt -> FamilienHausarzt &#0124; Hausarzt =>   
           [1-1 OUT](Bundle-1-1-ConsolidatedMedicationCard.json.html): FamilienHausarztAtHausarzt -> FamilienHausarzt &#0124; Hausarzt   
      * -> Patient => the resource can be taken from the input   
         * [1-1 PatAuthor IN](Parameters-1-1-PatAuthor-Input-Analyzer.json.html): AuthorMonikaWegmueller =>   
           [1-1 PatAuthor OUT](Bundle-1-1-PatAuthor-ConsolidatedMedicationCard.json.html): AuthorMonikaWegmueller  

#### Patient
##### Identifier
If there is the same patient with different identifiers in the [input documents](Parameters-A7-Input-Analyzer.json.html), then all identifiers will be listed with the patient in the [output document](Bundle-A7-ConsolidatedMedicationCard.json.html).

#### Info Input Document
The extension [Info Input Document](StructureDefinition-infoinputdocument.html) represents the information of the input document (source, type, date, id). This complexe extension contains these 4 extensions:
* [Input Document Source](StructureDefinition-inputdocumentsource.html) (Input document)
* [Input Document Type](StructureDefinition-inputdocumenttype.html) (Input document / Output document)
* [Input Document Date](StructureDefinition-inputdocumentdate.html) (Input document / Output document)
* [Input Document Id](StructureDefinition-inputdocumentid.html) (Input document / Output document)

The extension **Info Input Document** is set on each 'derivedFrom'-entry ([MedicationStatement](StructureDefinition-analyzer-medicationstatement.html), [MedicationRequest](StructureDefinition-analyzer-medicationrequest.html), [MedicationDispense](StructureDefinition-analyzer-medicationdispense.html), [Observation](StructureDefinition-analyzer-observationpadv.html)), but not on the [Header MedicationStatement](StructureDefinition-analyzer-medicationstatement-header.html).

##### Input Document Source
* **Analyzer Input**: This information is set or overwritten by the backend in each input document (see [Analyzer IN Composition](StructureDefinition-analyzer-in-composition.html)). (Note: This requirement must be considered if it is a different backend.)
* **Analyzer Output**: This information (from the input) is set on each 'derivedFrom'-entry, but not on the Header MedicationStatement.

##### Input Document Type
This information is used to distinguish the following document types:
* MTP/PRE/DIS/PADV: These document types have a unique codes (display values can vary!) that can be taken from the input document (`Composition.type`):
  * MTP: LOINC 77603-9
    ```json
   {
      "url" : "http://hcisolutions.ch/ig/analyzer/StructureDefinition/inputdocumenttype",
      "valueCodeableConcept" : {
         "coding" : [
            {
               "system" : "http://loinc.org",
               "code" : "77603-9",
               "display" : "Medication treatment plan.extended Document"
            }
         ]
      }
   }
   ```
  * PRE: LOINC 57833-6
  * DIS: LOINC 60593-1
  * PADV: LOINC 61356-2
* LIST/CARD: These documents types have the same code (`Composition.type`) and must therefore be differentiated via the title (`Composition.title`) (used afterwards to set the Input Document Id):
   * LIST/CARD: LOINC 56445-0
     * LIST: 'Medikationsliste' in german or 'Liste de médication' in french or 'Elenco delle terapie farmacologiche' in italian or Medication List' in english
     ```json
      {
         "url" : "http://hcisolutions.ch/ig/analyzer/StructureDefinition/inputdocumenttype",
         "valueCodeableConcept" : {
            "coding" : [
               {
                  "system" : "http://loinc.org",
                  "code" : "56445-0",
                  "display" : "Medication summary Document"
               }
            ],
            "text" : "Medication List"
         }
      }
      ```
     * CARD: 'Medikationsplan' in german or 'Plan de médication' in french or 'Piano farmacologico' in talian or 'Medication Card' in english
      ```json
      {
         "url" : "http://hcisolutions.ch/ig/analyzer/StructureDefinition/inputdocumenttype",
         "valueCodeableConcept" : {
            "coding" : [
               {
                  "system" : "http://loinc.org",
                  "code" : "56445-0",
                  "display" : "Medication summary Document"
               }
            ],
            "text" : "Medication Card"
         }
      }
      ```
     * If none of these titles is specified, the additional information (.text) is omitted.

##### Input Document Id
This information is needed, for example, when a medication is 'imported' via a LIST (input document), on which a PADV is to be created later (needs the reference externalDocumentId).   

The identifier is taken from the input document as follows:
* Input document = MTP/PRE/DIS/PADV/CARD => **Bundle.identifier** 
   * If the additional information for CARD `"text" : "Medication Card"` (`http://hcisolutions.ch/ig/analyzer/StructureDefinition/inputdocumenttype`) is missing, then follow the rules for LIST. It may happen that the externalDocumentId of another document (e.g. MTP) is used. This must be tolerated at the moment, as long as no other differentiation CARD/LIST is possible (<https://github.com/hl7ch/ch-emed/issues/140>). The drug will be referenced correctly in any case, e.g. in a later PADV.
* Input document = LIST
   * MedicationStatement => extension.url = **"externalDocumentId"** (valueIdentifier) from this extension: `http://fhir.ch/ig/ch-emed/StructureDefinition/ch-emed-ext-treatmentplan`
   * MedicationDispense => extension.url = **"externalDocumentId"** (valueIdentifier) from this extension: `http://fhir.ch/ig/ch-emed/StructureDefinition/ch-emed-ext-dispense`
   * MedicationRequest => extension.url = **"externalDocumentId"** (valueIdentifier) from this extension: `http://fhir.ch/ig/ch-emed/StructureDefinition/ch-emed-ext-prescription`
   * Observation => extension.url = **"externalDocumentId"** (valueIdentifier) from this extension: `http://fhir.ch/ig/ch-emed/StructureDefinition/ch-emed-ext-pharmaceuticaladvice`
   * <span style="color:red">Note: The presence of this information in the Medication List document is a requirement for the device that generates this document. If the information about the original document (externalDocumentId) is not included in the list, it will be lost. If a Medication Card document is used to initialize the device that generates the Medication List document, then the device must return this information afterwards, there is no reference back to the Medication Card document (Medication Card document is a snapshot and cannot be referenced according to the IHE Pharmacy Framework).</span>

{% include img.html img="infoinputdocument-mtp.png" caption="Fig.: Schematic illustration of the Info Input Document (MTP), the logic also applies to PRE/DIS/PADV/CARD" width="80%" %}

{% include img.html img="infoinputdocument-list.png" caption="Fig.: Schematic illustration of the Info Input Document (LIST)" width="80%" %}


#### History Changes
Codes to show the different type of changes in the medication history:
* [CodeSystem](CodeSystem-history-changes.html) & [ValueSet](ValueSet-history-changes.html)
* [ConceptMap](ConceptMap-ihe-padv-to-analyzer-history-changes.html) to show the mapping to the different types/codes of the PADV Observations (input document).


### FHIR Implementation Guide
#### Naming
The files (bundle & paramters) should all be named according to the same scheme, so that the analyzer tests can be performed in a standardized/automated way:
* Input document: `Parameters-<test-case-name>-Input-Analyzer.json`
* Output document:  `Bundle-<test-case-name>-ConsolidatedMedicationCard.json`    
Where &lt;test-case-name&gt; corresponds to the name of the test case. The test case will only be executed if an input/output pair with the same &lt;test-case-name&gt; is found.