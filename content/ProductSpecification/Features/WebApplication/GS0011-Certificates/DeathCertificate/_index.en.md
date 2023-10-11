---
title: Death Certificate
tags : ["Composing"]
---

## Introduction
Death Certificate is one of the basic features of the software product. Death Certificate feature provides the service of applying for the death certificate. One application number will be assigned to the each death certificate application. Death certificate application status can be tracked using application number.

## Business Assumptions
Death Certificate Feature should be planned at the design phase and updates to the death certificate at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Death Certificate feature is only accessible at the panchayat level.
1. While creating death certificate, applicant information will be stored.
1. Death Person Aadhaar Number is required to create death certificate.

### Non-functional Requirements
1. Death certificate should be tracked using Application Number or Applicant AadhaarId or Application Mobile Number.

### Problem Statement
1. Death certificate feature is required to provide the service of applying for death certificate.

### Design 
1. Each Death certificate has Death Person Information, Death Place Information, Death Details, and Applicant Information.
1. We can Create, Update, View, Track, and Remove the Death Certificate.
1. Death certificate status should be changed through update feature. And it's status should be monitored through Track feature.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|[gs0006-citizens]({{< ref "gs0006-citizens" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_death_certificate_list|To view all the death certificates|
|uc_death_certificate_search|To search the death certificate|
|uc_death_certificate_create|To create the death certificate|
|uc_death_certificate_update|To update the death certificate|
|uc_death_certificate_remove|To remove the death certificate|
|uc_death_certificate_view|To view the death certificate|
|uc_death_certificate_track|To track the death certificate|
|uc_death_certificate_export|To export the death certificate in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|Track|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|deathCitizenAid|YES|NA|0-9, maxlen=12|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "death_citizen_aid", referencedColumnName = "aid")|death_citizen_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|dateOfDeath|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "dc_dod", nullable = false)|dc_dod datetime DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|deathPlace|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "dc_death_place", length = 64, nullable = true)|dc_death_place varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|hospitalName|YES|NA|a-zA-Z0-9. _-, minlen=3, maxlen=64|@Column(name = "death_death_hospital_name", length = 64, nullable = true)|death_death_hospital_name varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|hospitalAddress|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=128|@Column(name = "death_death_hospital_address", length = 128, nullable = true)|death_death_hospital_address` varchar(128) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|deathDeathAddress|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=128|@Column(name = "death_death_address", length = 128, nullable = true)|death_death_address varchar(128) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|deathCause|YES|NA|Drop down values|@Enumerated(EnumType.STRING) @Column(name = "dc_death_cause", length = 64, nullable = true)|dc_death_cause varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|typeOfMedicalAttention|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "typeOfMedicalAttention", length = 64, nullable = true)|typeOfMedicalAttention varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|medicallyCertified|YES|NA|Boolean|@Column(name = "dc_medically_certified", nullable = true)|dc_medically_certified boolean DEFAULT false|YES|NO|YES|YES|NO|NO|NO||
|habituallySmoke|YES|NA|Boolean|@Column(name = "dc_habitually_smoke", nullable = true)|dc_habitually_smoke boolean DEFAULT false|YES|NO|YES|YES|NO|NO|NO||
|habituallyChewTobacco|YES|NA|Boolean|@Column(name = "dc_habitually_chew_tobacco", nullable = true)|dc_habitually_chew_tobacco boolean DEFAULT false|YES|NO|YES|YES|NO|NO|NO||
|habituallyChewArecaunt|YES|NA|Boolean|@Column(name = "dc_habitually_chew_arecaunt", nullable = true)|dc_habitually_chew_arecaunt boolean DEFAULT false|YES|NO|YES|YES|NO|NO|NO||
|habituallyDrinkAlcohol|YES|NA|Boolean|@Column(name = "dc_habitually_drink_alcohol", nullable = true)|dc_habitually_drink_alcohol boolean DEFAULT false|YES|NO|YES|YES|NO|NO|NO||
|applicantAid|YES|NA|0-9|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "applicant_aid", referencedColumnName = "aid")|applicant_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|YES|YES|YES||
|applicatName|YES|NA|a-zA-Z0-9_/ -., minlen=3, maxlen=64|@Column(name = "applicat_name", length = 64, nullable = false)|applicat_name varchar(64) NOT NULL|YES|NO|YES|YES|NO|YES|YES||
|applicantSurname|YES|NA|a-zA-Z0-9. _-, minlen=1, maxlen=32|@Column(name = "applicant_surname", length = 32, nullable = false)|applicant_surname varchar(32) NOT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantFSname|YES|NA|a-zA-Z0-9_/ -.,minlen=3, maxlen=64|@Column(name = "applicant_fsname", length = 64, nullable = false)|applicant_fsname varchar(64) NOT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantMobile|YES|NA|0-9|@Column(name = "applicant_mobile", length = 13, nullable = false)|applicant_mobile varchar(13) NOT NULL|YES|NO|YES|YES|YES|YES|YES||
|applicantEmail|YES|NA|a-zA-Z0-9._@|@Column(name = "applicant_email", length = 64, nullable = true, unique = true)|applicant_email varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|YES|NO||
|applicationNumber|NO|NA|a-zA-Z0-9|@Column(name = "application_number", length = 32, nullable = false)|application_number varchar(32) NOT NULL|NO|NO|NO|NO|YES|NO|YES||
|copyNo|YES|NA|Drop Down Values|@Column(name = "copy_no", nullable = true)|copy_no bigint(20) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|status|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "status_type", length = 16, nullable = true)|status_type varchar(16) DEFAULT NULL|NO|YES|YES|YES|YES|NO|YES||
|descr|YES|NA|a-zA-Z0-9/:#, _.-[]()@|@Column(name = "descr", length = 256, nullable = true)|descr varchar(256) DEFAULT NULL|NO|YES|YES|YES|YES|NO|NO||
|attachment|YES|NA|Attachment|@Column(name = "file_name", length = 36, nullable = false)|file_name varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO|NO||

#### ENUM CONSTANTS

##### Death Place

{{<mermaid align="left">}}
classDiagram
    class BirthDeathPlace{
      HOUSE
      HOSPITAL
      OTHER
    }
{{< /mermaid >}}

##### Death Cause

{{<mermaid align="left">}}
classDiagram
	class DeathCause{
		CHOLERA
 		TYPHOID_PARATYPHOID
		FOOD_POISIONING
		DYSENTRY_DIARRHOEA_GASTRIC_ENTERITIS
		TUBERCULOSIS
		LEPROSY
		DIPHTHERIA	
		WHOOPING_COUGH
		TETANUS
		ACUTE_POLIOMYELITIS
		MEASLES
		RABIES
		MALARIA
		CANCER
		DIABETIC_MELLITUS
		ANAEMIA
		MENINGITIS
		HEART_DISEASE_AND_HEART_ATTACKS
		PNEUMONIA
		INFLUENZA
		BRONCHITIS_AND_ASTHMA
		JAUNDICE
		CHRONIC_LIVER_DISEASE_AND_CIRRHOSIS
		ULCER_OF_STOMACH_AND_DUODENUM
		APPENDICITIES
		SYPHILIS_AND_OTHER_DISEASES_OF_GENITOURINARY_SYSTEM
		ABORTIONS
		COMPLICATIONS_RELATED_TO_PREGNANCY_CHILD_BIRTH_PUERPERIUM
		CEREBROVASCULAR_PARALYSIS
		SENILITY
		BITES_OR_STINGS_OF_VENOMOUS_ANIMAL
		ACCIDENTAL_BURNS
		FALLS_AND_DROWNING
		ACCIDENTAL_POISONING
		TRANSPORT_ACCIDENTS
		SUICIDE
		HOMICIDE
		CHICKEN_POX
		AGED_PERSON
		BLOOD_PRESSURE
		OLD_AGE
		KIDNEY_FAILURE
		NATURAL_DEATH
		BROUGHT_DEAD
		STATUS_EPILEPPPPPPTCUS_PULAMMARY_OCLEMA
		SUGAR
		SHORTNESS_OF_BREATH
		DROWNING
		BLOOD_VESSELS
		CORDIO_RESTORATING
		RESPIRATORY_FAILURE
		RHEUMATIC_DISEASE
		BRAIN_TUMER
		BLOOD_CANCER
		LIVER_FAILURE
		MATERNITY
		PARALYSIS_DISEASE
		MUCUS_BLOCKAGE
		EPILEPSY
		HEMIPARESIS
		CARDIAC_ARREST
		MURDER
		HIPER_TENSION
		BREATH_DISORDER
		ORGAN_FAILURE
		OTHER
	}
{{< /mermaid>}}

##### Type Of Medical Attention

{{<mermaid align="left">}}
classDiagram
    class TypeOfMedicalAttention{
    DOCTOR_NURSE_OR_TRAINED_MIDWIFE
    TRADITIONAL_BIRTH_ATTENDANT
    RELATIVES_AND_OTHERS
    NO_MEDICAL_ATTENTION
    INSTITUTIONAL_GOVT
    INSTITUTIONAL_PVT_NON_GOVT
 }
{{< /mermaid >}}

##### No of Copies

{{<mermaid align="left">}}
classDiagram
    class CopyNo{
		1
		2
		3
		4
		5
		6
		7
		8
		9
		10
    }
{{< /mermaid >}}

##### Certificate Status

{{<mermaid align="left">}}
classDiagram
    class CertificateStatus{
		OPEN
		IN_PROGRESS
		CLOSED
		HOLD
		REJECTED
    }
{{< /mermaid >}}



#### Feature Permission
|Permission code|Action|
|---------------|-------|
|||


#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Foreign Keys|1. fk__gs_citizenCert__death_citizen_aid FOREIGN KEY (death_citizen_aid) REFERENCES gs_citizen (aid)|
||2. 3. fk__gs_citizenCert__applicant_aid FOREIGN KEY (applicant_aid) REFERENCES gs_citizen (aid)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|||

## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Track page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreteBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---TrackBtn[Track]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	DeathCertificateMenu((Death Certificate Menu))
	ListPage{Death Certificate List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    TrackPage((Track Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->DeathCertificateMenu
    subgraph Menu
    DeathCertificateMenu
	end
	subgraph List
	DeathCertificateMenu-->ListPage
	ListPage--C-U-R-V-T-E-->ListPage
	end
	subgraph Error
	DeathCertificateMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph Create
	ListPage--C-->CreatePage
	CreatePage--SB-->ListPage
	CreatePage--SB-->CreatePage
	end
	subgraph Update
	ListPage--U-->UpdatePage
	UpdatePage--SB-->ListPage
	UpdatePage--SB-->UpdatePage
	end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--B-->ListPage
	ViewPage--B-->ViewPage
	end
	subgraph Remove
	ListPage--R-->RemovePage
	RemovePage--SB-->ListPage
	RemovePage--SB-->RemovePage
	end
	subgraph Download
    ListPage--E-->DownloadFile
    end
    subgraph Track
	ListPage--T-->TrackPage
	TrackPage--SB-->ListPage
	TrackPage--SB-->TrackPage
	end
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 9 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px;
    linkStyle 12 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    linkStyle 15 stroke:green,stroke-width:2px;
    linkStyle 17 stroke:green,stroke-width:2px; 
    linkStyle 18 stroke:green,stroke-width:2px;
    linkStyle 19 stroke:green,stroke-width:2px;    
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
    linkStyle 20 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|Create|
|U|Update|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|F|Failure|
|T|Track|
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-V-T-E|Create or Update or Remove or View or Track or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant DeathCertificateListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/ctx/DeathCertificate/list ListPage
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S:  GET /app/ctx/DeathCertificate/list ListPage
        cloud-->>-DeathCertificateListPage: RES: List Page
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/create/form CreateFormPage
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/create/form CreateFormPage
        cloud-->>-DeathCertificateListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, POST /app/DeathCertificate/create Create
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : POST /app/DeathCertificate/create Create
        cloud-->>-DeathCertificateListPage: RES: An Death Certificate Successfully Created
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/update/form UpdateFormPage
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/update/form UpdateFormPage
        cloud-->>-DeathCertificateListPage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, POST /app/DeathCertificate/update update
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : POST /app/DeathCertificate/update Update
        cloud-->>-DeathCertificateListPage: RES: An Death Certificate Successfully Updated
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/remove/form RemoveFormPage
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/remove/form RemoveFormPage
        cloud-->>-DeathCertificateListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, POST /app/DeathCertificate/remove Remove
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : POST /app/DeathCertificate/remove Remove
        cloud-->>-DeathCertificateListPage: RES: An Death Certificate Successfully Removed
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/track/form TrackFormPage
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/track/form TrackFormPage
        cloud-->>-DeathCertificateListPage: RES : Track Form Loaded
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, POST /app/DeathCertificate/track Track
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : POST /app/DeathCertificate/track Track
        cloud-->>-DeathCertificateListPage: RES: Death certificate Object
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/view ViewPage
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/view ViewPage
        cloud-->>-DeathCertificateListPage: RES: deathCertificate View
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/exportPdf ExportPdf
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/exportPdf ExportPdf
        cloud-->>-DeathCertificateListPage: RES: deathCertificate Pdf
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/exportListPdf ExportListPdf
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/exportListPdf ExportListPdf
        cloud-->>-DeathCertificateListPage: RES: deathCertificate List Pdf
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/exportXlx ExportXlx
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/exportXlx ExportXlx
        cloud-->>-DeathCertificateListPage: RES: deathCertificate Xlx
    end
    rect rgb(244,244,244)
        DeathCertificateListPage->>+Net: Check Internet, GET /app/DeathCertificate/exportListXlx ExportListXlx
        Net--x-DeathCertificateListPage: F : Connection Error
        DeathCertificateListPage->>+cloud: S : GET /app/DeathCertificate/exportListXlx ExportListXlx
        cloud-->>-DeathCertificateListPage: RES: deathCertificate List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|1.0|ut_p_c_deathCert_ideal ||
|1.0|ut_p_c_deathCert_input_validate||
|1.0|ut_n_c_deathCert_input_validate||
|1.0|ut_p_c_deathCert_captcha||
|1.0|ut_n_c_deathCert_captcha||
|1.0|ut_p_c_deathCert_death_citizen_aid||
|1.0|ut_n_c_deathCert_death_citizen_aid||
|1.0|ut_p_c_deathCert_applicant_aid||
|1.0|ut_n_c_deathCert_applicant_aid||
|1.0|ut_p_u_deathCert_ideal ||
|1.0|ut_p_u_deathCert_input_validate||
|1.0|ut_n_u_deathCert_input_validate||
|1.0|ut_p_u_deathCert_captcha||
|1.0|ut_n_u_deathCert_captcha||
|1.0|ut_p_r_deathCert_ideal ||
|1.0|ut_p_r_deathCert_input_validate||
|1.0|ut_n_r_deathCert_input_validate||
|1.0|ut_p_r_deathCert_captcha||
|1.0|ut_n_r_deathCert_captcha||
|1.0|ut_p_t_deathCert_ideal ||
|1.0|ut_p_t_deathCert_captcha||
|1.0|ut_n_t_deathCert_captcha||

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Death Certificate should be provided in the User Manual.

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

## Development Estimations
|Release Tag|Feature/Defect ID|Scrum Deatils|Start date|End date|
|-----------|-----------------|-------------|----------|--------|
|2020OCT|GS-0002|Scrum 2020OCTs2|14 OCT 2020|28 OCT 2020|

## Feature Doneness Criteria
Check list for the Doneness criteria

|Metric|Unit Measure|Expected Result|Actual Result|Accepted?|Remarks|Approver|
|------|------------|---------------|-------------|---------|-------|----------|
|Acceptance Criteria Defined?|YES or NO|YES|YES|Accepted|All test cases passed|PM|
|Architecture Approved?|YES or NO|YES|YES|Accepted|Design is accepted|Architect|
|Coding Completed?|YES or NO|YES|YES|Completed|Completed|EM|
|Product Defects|Number|0|0|Accepted||EM|
|Unit Test Case Count?|Number|>5|8|Accepted|Tested|EM|
|Integration Test Cases Count|Number|>5|9|Accepted|Tested|EM|
|Sonar Vulnerabilities Count|Number|0|0|Accepted|validated|EM|
|Code Coverage|Number|>98%|99%|Accepted|Validated|EM|
|User Manual Verified?|YES or NO|YES|YES|Accepted|Validated|DocM|
|PenTest Defect Count?|Number|<2|0|Accepted|Validated|EM|
|PM Accepted?|YES or NO|YES|YES|Accepted|Good to go|PM|
|OM Accepted?|YES or NO|YES|YES|Accepted|Good to go|OM|
|Deployed to Staging?|YES or NO|YES|YES|Accepted|Good to go|EM|
|Deployed to Production?|YES or NO|YES|YES|Accepted|Good to go|OM|




 
