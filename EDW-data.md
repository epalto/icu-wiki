# Electronic Data Warehouse (EDW) documentation
EDW contains all the information from EPIC and other storage sources. Accessing only to the EPIC source is enough to get 
all the necessary EMR. Note that data have different formats, from numerical values to images, strings or physician notes. 
One important feature to consider is that numerical data is not continuous (it is not sampled in a high frequency rate), 
since the values stored have been previously approved by a nurse or measured by a physician.

## Table of Contents
1. [Accessing to EDW database and running queries](#accessing-to-edw-database-and-running-queries)
2. [Common tables obtained from EDW](#common-tables-obtained-from-edw)

### Accessing to EDW database and running queries
Once having access to EDW, go to [Partners Citrix workspace](https://workspace.partners.org/Citrix/UniversalWeb/). Then, 
find the app "SQL Server 2014 Management Studio", where `SQL` queries can be performed to pull patients' data.

For information about SQL programming language, the following [cheat sheet](https://www.sqltutorial.org/sql-cheat-sheet/)
provides the most general and useful commands. Extra help can be found in this 3 hour [video tutorial](https://www.youtube.com/watch?v=7S_tz1z_5bA). 
Moreover, information about data elements and where to find them is included in 
the [EDW Atlas](https://enterpriseanalytics.partners.org/atlas).

### Common tables obtained from EDW
Patients' information is usually organized in several tables, obtaining a set of `.csv` files. They can be opened and 
treated with `Python` library `pandas`. 

The most common tables are:

* Admission-vitals
    * Contains a lookup of patient vital signs at admission stage.

* ADT (Admission Discharge Transfer) 
    * Contains a time-series of patient movement per MRN or CSN.
    
* Demographics
    * Contains a lookup of patient demographics.
    
* Diagnosis 
    * Contains a time-series of diagnosis per MRN or CSN.

* Flowsheet
    * Contains a time-series of patient chart-review-items contained within a MRN or CSN.

* Labs
    * Contains a time-series of patient lab values contained within a MRN or CSN.

* Medication
    * Contains a time-series of patient medication administration per MRN or CSN.

* Medication-order
    * Contains a time-series of patient medication order per MRN or CSN.


<details><summary>Click here to see the items included in the general structure of those files:</summary>


| Table Name | Parameter Name | Type | Description|
| --- | --- | --- | --- |
| Admission-vitals | | |
|  | PatientEncounterID | Integer |  |
|  | HospitalAdmitDTS | Time Stamp |  |
|  | HospitalDischargeDTS | Time Stamp |  |
|  | HospitalAdmitTypeCD | Integer |  |
|  | HospitalAdmitTypeDSC | String |  |
|  | TemperatureFahrenheitNBR | Float |
|  | HeartRateNBR | Integer |  |
|  | BloodPressureSystolicNBR | Integer |  |
|  | BloodPressureDiastolicNBR | Integer |  |
|  | RespirationRateNBR | Integer |  |
|  | WeightPoundNBR | Integer |  |
|  | HeightTXT | String |  |
|  | BodyMassIndexNBR | Integer |  |
| ADT |  |  |  |
|  | MRN | Integer |  |
|  | PatientEncounterID | Integer |  |
|  | DepartmentID | Integer |  |
|  | Room | Integer |  | 
|  | Bed | Integer |  |
|  | HospitalAdmitDTS | Time Stamp |  |
|  | HospitalDischargeDTS | Time Stamp |  |
|  | TransferInDTS | Time Stamp |  |
|  | TransferOutDTS | Time Stamp |  | 
|  | ADTEventTypeCD | Integer |  |
|  | ADTEventTypeDSC | String  |  |
|  | ADTEventSubtypeCD | Integer |  |
|  | ADTEventSubtypeDSC | String |  |
|  | DepartmentID | Integer |  |
|  | DepartmentDSC | String |  | 
|  | EffectiveDTS | Time Stamp |  |
|  | EventDTS | Time Stamp |  |
|  | PatientClassCD | Integer |  |
|  | PatientClassDSC | String |  | 
|  | PatientServiceCD | Integer |  |
|  | PatientServiceDSC | String |  |
|  | OriginalEventSubtypeDTS | Time Stamp |  |
|  | OriginalEffectiveDTS | Time Stamp |  |
| Demographics |  |  |  |
|  | MRN | Integer |  |
|  | PatientID | String |  |
|  | PatientEncounterID | Integer |  |
|  | PatientRaceCD | Integer |  |
|  | PatientRaceDSC | String |  |
|  | BirthDTS | Time Stamp |  |
|  | DeathDTS | Time Stamp |  |
|  | EthnicGroupCD | Integer |  |
|  | EthnicGroupDSC | String |  |
|  | MaritalStatusCD | Integer |  |
|  | MaritalStatusDSC | String |  |
|  | PatientStatusCD | Integer |  |
|  | PatientStatusDSC | String |  |
|  | SexCD | Integer |  |
|  | SexDSC | String |  |
| Diagnosis |  |  |  |
|  | MRN | Integer |  |
|  | PatientEncounterID | Integer |  |
|  | DiagnosisID | Integer |  |
|  | DiagnosisNM | String |  |
|  | ICD9CD_1 | Integer |  |
|  | ICD9_DSC | String |  |
|  | PatientClassDSC | String |  |
|  | PatientClassCD | Integer |  |
|  | PatientServiceDSC | String |  |
|  | PatientServiceCD | Integer |  |
|  | ADTPatientClassificationCD | Integer |  |
|  | ADTPatientClassificationDSC | String |  |
|  | ContactDTS | Time Stamp |  |
|  | MapID | Integer |  |
|  | ICD9 | Integer |  |
|  | ICD9DSC | String |  |
|  | ICD9DottedCD | Float |  |
|  | TypeCD | String |  |
|  | ICD10 | String |  |
|  | ICD10DSC | String |  |
|  | ICD10DottedCD | String |  |
| Flowsheet |  |  |  |
|  | MRN | Integer |  |
|  | PatientID | String |  |
|  | PatientEncounterID | Integer |  |
|  | DepartmentID | Integer |  |
|  | FlowsheetDataID | Integer |  |
|  | FlowsheetMeasureID | Integer |  |
|  | FlowsheetMeasureNM | String |  |
|  | RecordedDTS | Time Stamp |  |
|  | EntryTimeDTS | Time Stamp |  |
|  | MeasureTXT | String |  |
|  | MeasureCommentTXT | String |  |
|  | ValueTypeCD | Integer |  |
|  | ValueTypeDSC | String |  |
|  | UnitsCD | String |  |
|  | DisplayNM | String |  |
|  | DisplayAbbreviationCD | String |  |
| Labs |  |  |  |
|  | PatientIdentityID | Integer |  |
|  | PatientID | String |  |
|  | PatientEncounterID | Integer |  |
|  | OrderProcedureID | Integer |  |
|  | OrderingDTS | Time Stamp |  |
|  | OrderDTS | Time Stamp |  |
|  | OrderTimeDTS | Time Stamp |  |
|  | StartDTS | Time Stamp |  |
|  | EndDTS | Time Stamp |  |
|  | ResultDateDTS | Time Stamp |  |
|  | ResultDTS | Time Stamp |  |
|  | OrderTypeCD | Integer |  |
|  | OrderTypeDSC | String |  |
|  | OrderDisplayNM | String |  |
|  | ProcedureID | Integer |  |
|  | ProcedureDSC | String |  |
|  | ComponentID | Integer |  |
|  | ComponentCommentTXT | String |  |
|  | ComponentNM | String |  |
|  | ComponentCommonNM | String |  |
|  | ResultTXT | String |  |
|  | ResultValueNBR | String |  |
|  | LOINCTXT | String |  |
|  | LabStatusDSC | String |  |
|  | OrderStatusDSC | String |  |
|  | ReferenceRangeUnitCD | String |  |
|  | ResultStatusDSC | String |  |
|  | LabTechnicianID | String |  |
|  | DataTypeCD | Integer |  |
|  | DataTypeDSC | String |  |
|  | ComponentObservedDTS | Time Stamp |  |
|  | SpecimenReceivedTimeDTS | Time Stamp |  |
|  | SpecimenTakenTimeDTS | Time Stamp |  |
|  | SpecimenCommentsTXT | String |  |
| Medication |  |  |  |
|  | OrderStatusCD | Integer |  |
|  | OrderStatusDSC | String |  |
|  | OrderID | Integer |  |
|  | MRN | Integer |  |
|  | PatientEncounterID | Integer |  |
|  | MedicationID | Integer |  |
|  | MedicationDSC | String |  |
|  | OrderInstantDTS | Time Stamp |  |
|  | OrderStartDTS | Time Stamp |  |
|  | OrderEndDTS | Time Stamp |  |
|  | DoseUnitCD | Integer |  |
|  | DoseUnitDSC | String |  |
|  | MinimumDoseAMT | Integer |  |
|  | MaximumDoseAMT | Integer |  |
|  | PatientLocationID | Integer |  |
|  | PatientLocationDSC | String |  |
|  | MedicationTakenDTS | Time Stamp |  |
|  | MARActionCD | Integer |  |
|  | MARActionDSC | String |  |
|  | RouteDSC | String |  |
|  | RouteCD | Integer |  |
|  | SiteCD | Integer |  |
|  | SiteDSC | String |  |
|  | InfusionRateNBR | Float |  |
|  | InfusionRateUnitCD | Integer |  |
|  | InfusionRateUnitDSC | String |  |
|  | DurationNBR | Float |  |
|  | DurationUnitCD | Integer |  |
|  | DurationUnitDSC | String |  |
|  | SigTXT | String |  |
|  | PrescriptionQuantityNBR | String |  |
|  | MedicationDiscontinueReasonDSC | String |  |
|  | DiscreteFrequencyDSC | String |  |
|  | DiscreteDoseAMT | Float |  |
|  | DiscreteDispenseUnitDSC | String |  |
| Medication-order |  |  |  |
|  | OrderID | Integer |  |
|  | PatientID | String |  |
|  | PatientEncounterID | Integer |  |
|  | OrderDTS | Time Stamp |  |
|  | OrderInstantDTS | Time Stamp |  |
|  | PharmacyID | Integer |  |
|  | OrderCreatorUserID | Integer |  |
|  | MedicationID | Integer |  |
|  | MedicationDSC | String |  |
|  | StartDTS | Time Stamp |  |
|  | EndDTS | Time Stamp |  |

</details>
