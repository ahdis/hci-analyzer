### Anwendungsfälle CH EMED
Die in diesem Abschnitt abgebildeten Anwendungsfälle basieren auf dem Fallbeispiel ([de](http://fhir.ch/ig/ch-emed/usecase-german.html), [fr](http://fhir.ch/ig/ch-emed/usecase-french.html)), welches im CH EMED Implementierungsleitfaden abgebildet ist. Die Inputdokumente für den Analyzer sind von dort übernommen.

#### 1-1 Therapieentscheid Medikation (Medication Treatment Plan document)
* [1-1 Input Analyzer](Parameters-1-1-Input-Analyzer.html)
   * Inputdokument: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html)
* [1-1 Consolidated Medication Card document](Bundle-1-1-ConsolidatedMedicationCard.html) 

#### 1-2 Abgabe (Medication Dispense document)
* [1-2 Input Analyzer](Parameters-1-2-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html)
* [1-2 Consolidated Medication Card document](Bundle-1-2-ConsolidatedMedicationCard.html)

#### 2-1 Medikationsliste (Medication List document)
Arbeitshypothese: Die Medikationsliste ist ein dynamisch generiertes Dokument und wird daher nicht als Inputdokument für den Analyzer auftreten.


#### 2-2 Kommentar zur Medikation (Pharmaceutical Advice document)
* [2-2 Input Analyzer](Parameters-2-2-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html), [2-2 PADV](http://fhir.ch/ig/ch-emed/Bundle-2-2-PharmaceuticalAdvice.html)
* [2-2 Consolidated Medication Card document](Bundle-2-2-ConsolidatedMedicationCard.html)

#### 2-3 Therapieentscheid Medikation (Medication Treatment Plan document)
* [2-3 Input Analyzer](Parameters-2-3-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html), [2-2 PADV](http://fhir.ch/ig/ch-emed/Bundle-2-2-PharmaceuticalAdvice.html), [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html)
* [2-3 Consolidated Medication Card document](Bundle-2-3-ConsolidatedMedicationCard.html)

##### Testfall Beloc Zok: Therapieentscheid Beloc Zok
Abgesetztes Triatec wird für Testzwecke nicht aufgeführt.
* [Input Analyzer](Parameters-BeloczokMTP-Input-Analyzer.html)
   * Inputdokument: [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html)
* [Consolidated Medication Card document](Bundle-BeloczokMTP-ConsolidatedMedicationCard.html)

#### 2-4 Abgabe (Medication Dispense document)
* [2-4 Input Analyzer](Parameters-2-4-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html), [2-2 PADV](http://fhir.ch/ig/ch-emed/Bundle-2-2-PharmaceuticalAdvice.html), [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html), [2-4 DIS](http://fhir.ch/ig/ch-emed/Bundle-2-4-MedicationDispense.html)
* [2-4 Consolidated Medication Card document](Bundle-2-4-ConsolidatedMedicationCard.html)

##### Testfall Beloc Zok: Abgabe Beloc Zok
Abgesetztes Triatec wird für Testzwecke nicht aufgeführt.
* [Input Analyzer](Parameters-BeloczokDIS-Input-Analyzer.html)
   * Inputdokumente: [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html), [2-4 DIS](http://fhir.ch/ig/ch-emed/Bundle-2-4-MedicationDispense.html)
* [Consolidated Medication Card document](Bundle-BeloczokDIS-ConsolidatedMedicationCard.html)

#### 2-5 Therapieentscheid Medikation (Medication Treatment Plan document)
* [2-5 Input Analyzer](Parameters-2-5-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html), [2-2 PADV](http://fhir.ch/ig/ch-emed/Bundle-2-2-PharmaceuticalAdvice.html), [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html), [2-4 DIS](http://fhir.ch/ig/ch-emed/Bundle-2-4-MedicationDispense.html), [2-5 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-5-MedicationTreatmentPlan.html)
* [2-5 Consolidated Medication Card document](Bundle-2-5-ConsolidatedMedicationCard.html)

##### Testfall Norvasc: Therapieentscheid Norvasc
Abgesetztes Triatec und abgegebenes Beloc Zok werden für Testzwecke nicht aufgeführt.
* [Input Analyzer](Parameters-NorvascMTP-Input-Analyzer.html)
   * Inputdokument: [2-5 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-5-MedicationTreatmentPlan.html)
* [Consolidated Medication Card document](Bundle-NorvascMTP-ConsolidatedMedicationCard.html)

#### 2-6 Rezept (Medication Prescription document)
* [2-6 Input Analyzer](Parameters-2-6-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html), [2-2 PADV](http://fhir.ch/ig/ch-emed/Bundle-2-2-PharmaceuticalAdvice.html), [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html), [2-4 DIS](http://fhir.ch/ig/ch-emed/Bundle-2-4-MedicationDispense.html), [2-5 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-5-MedicationTreatmentPlan.html), [2-6 PRE](http://fhir.ch/ig/ch-emed/Bundle-2-6-MedicationPrescription.html)
* [2-6 Consolidated Medication Card document](Bundle-2-6-ConsolidatedMedicationCard.html)

##### Testfall Norvasc: Rezept Norvasc
Abgesetztes Triatec und abgegebenes Beloc Zok werden für Testzwecke nicht aufgeführt.
* [Input Analyzer](Parameters-NorvascPRE-Input-Analyzer.html)
   * Inputdokumente: [2-5 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-5-MedicationTreatmentPlan.html), [2-6 PRE](http://fhir.ch/ig/ch-emed/Bundle-2-6-MedicationPrescription.html)
* [Consolidated Medication Card document](Bundle-NorvascPRE-ConsolidatedMedicationCard.html)

#### 2-7 Medikationsplan (Medication Card document)
* [2-7 Input Analyzer](Parameters-2-7-Input-Analyzer.html)
   * Inputdokumente: [1-1 MTP](http://fhir.ch/ig/ch-emed/Bundle-1-1-MedicationTreatmentPlan.html), [1-2 DIS](http://fhir.ch/ig/ch-emed/Bundle-1-2-MedicationDispense.html), [2-2 PADV](http://fhir.ch/ig/ch-emed/Bundle-2-2-PharmaceuticalAdvice.html), [2-3 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-3-MedicationTreatmentPlan.html), [2-4 DIS](http://fhir.ch/ig/ch-emed/Bundle-2-4-MedicationDispense.html), [2-5 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-5-MedicationTreatmentPlan.html), [2-6 PRE](http://fhir.ch/ig/ch-emed/Bundle-2-6-MedicationPrescription.html), [2-7 Card](http://fhir.ch/ig/ch-emed/Bundle-2-7-MedicationCard.html)
* [2-7 Consolidated Medication Card document](Bundle-2-7-ConsolidatedMedicationCard.html)

##### Testfall Norvasc: Medikationsplan Norvasc
Abgesetztes Triatec und abgegebenes Beloc Zok werden für Testzwecke nicht aufgeführt.
* [Input Analyzer](Parameters-NorvascCard-Input-Analyzer.html)
   * Inputdokumente: [2-5 MTP](http://fhir.ch/ig/ch-emed/Bundle-2-5-MedicationTreatmentPlan.html), [2-6 PRE](http://fhir.ch/ig/ch-emed/Bundle-2-6-MedicationPrescription.html), [2-7 Card](http://fhir.ch/ig/ch-emed/Bundle-2-7-MedicationCard.html) (nur Norvasc)
* [Consolidated Medication Card document](Bundle-NorvascCard-ConsolidatedMedicationCard.html)

### Anwendungsfälle zur Illustration der Art der Veränderung

Die Art der Veränderung sind im [ValueSet History Changes](ValueSet-history-changes.html) definiert.

#### A1 Substitution
Apotheke Gare führt eine Substituion bei Zocor durch.
* [A1 Input Analyzer](Parameters-A1-Input-Analyzer.html)
   * Inputdokumente: Medication Card Zocor, Medication Card Simcora
* [A1 Consolidated Medication Card document](Bundle-A1-ConsolidatedMedicationCard.html)

#### A2 Gleiche Medikation, Änderung Arzt
Ausgangsmedikation Valium 5 mg Dosierung 0-0-0-2 (Dr. Dupont) und Änderung Valium 10 mg 0-0-0-1 (Apotheke Gare).
* [A2 Input Analyzer](Parameters-A2-Input-Analyzer.html)
   * Inputdokumente: Medication Card Valium 2 x 5 mg, Medication Card Valium 1 x 10 mg
* [A2 Consolidated Medication Card document](Bundle-A2-ConsolidatedMedicationCard.html)

#### A3 Änderung Dosierung
Arzt Dr. Dupont ändert Dosierung bei Reniten von morgens 1 Tbl. zu morgens 2 Tbl.
* [A3 Input Analyzer](Parameters-A3-Input-Analyzer.html)
   * Inputdokumente: Medication Card Reniten 1 Tbl. morgens, Medication Card Reniten 2 Tbl. morgens
* [A3 Consolidated Medication Card document](Bundle-A3-ConsolidatedMedicationCard.html)

#### A4 Änderung Arzt
Dr. Dupont verschreibt am 01.03.2020 das Medikament Reniten. Ab 10.03.2020 verschreibt Dr. Monney das Medikament weiter.
* [A4 Input Analyzer](Parameters-A4-Input-Analyzer.html)
   * Inputdokumente: Medication Card Dr. Dupont, Medication Card Dr. Monney
* [A4 Consolidated Medication Card document](Bundle-A4-ConsolidatedMedicationCard.html)

#### A5 Änderung Therapie
Dr. Monney verschreibt neu das Medikamente Exforge. Ausgangsmedikation war Reniten, das nun abgesetzt wurde.
* [A5 Input Analyzer](Parameters-A5-Input-Analyzer.html)
   * Inputdokumente: Medication Card Reniten, Medication Card Exforge
* [A5 Consolidated Medication Card document](Bundle-A5-ConsolidatedMedicationCard.html)

#### A6 Änderung ROA (Route of Administration)
Arzt Dr. Dupont verschreibt zusätzlich ein Imigran Spray zu den bestehenden Imigran Tabletten.
* [A6 Input Analyzer](Parameters-A6-Input-Analyzer.html)
   * Inputdokumente: Medication Card Imigran Tabletten, Medication Card Imigran Tabletten und Spray
* [A6 Consolidated Medication Card document](Bundle-A6-ConsolidatedMedicationCard.html)

#### A7 Änderung Galenik
Arzt Dr. Dupont verordnet zusätzlich zu den Brufen Tabletten (600 mg) die Brufen retard Tabletten (800 mg).
* [A7 Input Analyzer](Parameters-A7-Input-Analyzer.html)
   * Inputdokumente: Medication Card Brufen (600 mg), Medication Card Brufen (600 mg) und Brufen retard (800 mg)
* [A7 Consolidated Medication Card document](Bundle-A7-ConsolidatedMedicationCard.html)