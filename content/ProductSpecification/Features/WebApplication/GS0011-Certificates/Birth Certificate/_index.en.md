---
title: Birth Certificate
tags : ["Composing"]
---

## Introduction
Birth Certificate is one of the basic features of the software product. Birth Certificate feature provides the service of applying for the birth certificate. One application number will be assigned to the each birth certificate application. Birth certificate application status can be tracked using application number.

## Business Assumptions
Birth Certificate Feature should be planned at the design phase and updates to the birth certificate at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Birth Certificate feature only accessible at the panchayat level.
1. While creating birth certificate, applicant information will be stored.
1. Father and Mother infomation is required to create the birth certificate application.

### Non-functional Requirements
1. Birth certificate should be tracked using Application Number or Applicant AadhaarId or Application Mobile Number.

### Problem Statement
1. Birth certificate feature is required to provide the service of applying for birth certificate.

### Design 
1. Each Birth certificate has  Child Information, Birth Place Information, and Applicant Information.
1. We can Create, Update, View, Track, and Remove the Birth Certificate.
1. Birth certificate status should be changed through update feature. And it's status should be monitored through Track feature.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|[gs0006-citizens]({{< ref "gs0006-citizens" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_birth_certificate_list|To view all the birth certificates|
|uc_birth_certificate_search|To search the birth certificate|
|uc_birth_certificate_create|To create the birth certificate|
|uc_birth_certificate_update|To update the birth certificate|
|uc_birth_certificate_remove|To remove the birth certificate|
|uc_birth_certificate_view|To view the birth certificate|
|uc_birth_certificate_track|To track the birth certificate|
|uc_birth_certificate_export|To export the birth certificate in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|Track|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|bcname|YES|NA|a-zA-Z0-9_/ -.,minlen=3, maxlen=64|@Column(name = "bc_name", length = 64, nullable = true)|bc_name varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|bcsurname|YES|NA|a-zA-Z0-9. _-, minlen=1, maxlen=32|@Column(name = "bc_surname", length = 32, nullable = true)|bc_surname varchar(32) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|bcgender|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "bc_gender", length = 8, nullable = true)|bc_gender varchar(8) DEFAULT NULL|YES|NO|YES|YES|NO|NO|YES||
|bcdob|YES|NA|Date Time|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "bc_dob", nullable = false)|bc_dob datetime DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|bcfatherAid|YES|NA|0-9|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "bc_faid", referencedColumnName = "aid")|bc_faid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|bcmotherAid|YES|NA|0-9|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "bc_maid", referencedColumnName = "aid")|bc_maid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|bloodGroupType|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "blood_group_type", length = 16, nullable = true)|blood_group_type varchar(16) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|birthPlace|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "bc_birth_place", length = 64, nullable = true)|bc_birth_place varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|YES||
|hospitalName|YES|NA|a-zA-Z0-9. _-|@Column(name = "birth_death_hospital_name", length = 64, nullable = true)|birth_death_hospital_name varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|YES||
|hospitalAddress|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=128|@Column(name = "birth_death_hospital_address", length = 128, nullable = true)|birth_death_hospital_address varchar(128) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|birthDeathAddress|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=128|@Column(name = "birth_death_address", length = 128, nullable = true)|birth_death_address varchar(128) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|childWeight|YES|NA|0-9.|@Column(name = "bc_child_weight", nullable = true)|bc_child_weight float(16,2) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|methodOfDelivery|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "bc_methodOfDelivery", length = 16, nullable = true)|bc_methodOfDelivery varchar(16) DEFAULT NULL|YES|NO|YES|YES|NO|NO|YES||
|typeOfMedicalAttention|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "typeOfMedicalAttention", length = 64, nullable = true)|typeOfMedicalAttention varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|pregnancyDuration|YES|NA|Drop Down Values|@Column(name = "bc_pregnancy_duration", nullable = true)|bc_pregnancy_duration bigint(20) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantAid|YES|NA|0-9|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "applicant_aid", referencedColumnName = "aid")|applicant_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|YES|YES|YES||
|applicatName|YES|NA|a-zA-Z0-9_/ -.,minlen=3, maxlen=64|@Column(name = "applicat_name", length = 64, nullable = false)|applicat_name varchar(64) NOT NULL|YES|NO|YES|YES|NO|YES|YES||
|applicantSurname|YES|NA|a-zA-Z0-9. _-, minlen=1, maxlen=32|@Column(name = "applicant_surname", length = 32, nullable = false)|applicant_surname varchar(32) NOT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantFSname|YES|NA|a-zA-Z0-9_/ -.,minlen=3, maxlen=64|@Column(name = "applicant_fsname", length = 64, nullable = false)|applicant_fsname varchar(64) NOT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantMobile|YES|NA|0-9|@Column(name = "applicant_mobile", length = 13, nullable = false)|applicant_mobile varchar(13) NOT NULL|YES|NO|YES|YES|YES|YES|YES||
|applicantEmail|YES|NA|a-zA-Z0-9._@|@Column(name = "applicant_email", length = 64, nullable = true, unique = true)|applicant_email varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|YES|NO||
|applicationNumber|NO|NA|a-zA-Z0-9._@|@Column(name = "application_number", length = 32, nullable = false)|application_number varchar(32) NOT NULL|NO|NO|NO|YES|YES|NO|YES||
|copyNo|YES|NA|Drop Down Values|@Column(name = "copy_no", nullable = true)|copy_no bigint(20) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|status|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "status_type", length = 16, nullable = true)|status_type varchar(16) DEFAULT NULL|NO|YES|YES|YES|NO|NO|YES||
|descr|YES|NA|a-zA-Z0-9/:#, _.-[]()@|@Column(name = "descr", length = 256, nullable = true)|descr varchar(256) DEFAULT NULL|NO|YES|YES|YES|NO|NO|NO||
|attachment|YES|NA|Attachment|@Column(name = "file_name", length = 36, nullable = false)|file_name varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO|NO||

#### ENUM CONSTANTS

##### Gender

{{<mermaid align="left">}}
classDiagram
    class GenderType{
      MALE
      FEMALE
      OTHER
    }
{{< /mermaid >}}

##### Blood Group Type

{{<mermaid align="left">}}
classDiagram
    class BloodGroup{
      A_POSITIVE
      A_NEGATIVE
      B_POSITIVE
      B_NEGATIVE
      O_POSITIVE
      O_NEGATIVE
      AB_POSITIVE
      AB_NEGATIVE
    }
{{< /mermaid >}}

##### Birth Place

{{<mermaid align="left">}}
classDiagram
    class BirthPlace{
      HOUSE
      HOSPITAL
      OTHER
    }
{{< /mermaid >}}

##### Method Of Delivery

{{<mermaid align="left">}}
classDiagram
    class MethodOfDelivery{
      NORMAL
      CESERAIN
      FORCEPS
      VACCUM_DELIVER_EPISIOTOMY
      LABOUR_NATURAL
    }
{{< /mermaid >}}

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

##### Pregnancy Duration

{{<mermaid align="left">}}
classDiagram
    class PregnancyDuration{
    	24
		25
		26
		27
		28
		29
		30
		31
		32
		33
		34
		35
		36
		37
		38
		39
		40
		41
		42
		43
		44
		45
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
|Unique Keys|gs_citizenCert__geoid (geoid)|
|Foreign Keys|1. fk__gs_citizenCert__bc_faid FOREIGN KEY (bc_faid) REFERENCES gs_citizen (aid)|
||2. fk__gs_citizenCert__bc_maid FOREIGN KEY (bc_maid) REFERENCES gs_citizen (aid)|
||3. fk__gs_citizenCert__applicant_aid FOREIGN KEY (applicant_aid) REFERENCES gs_citizen (aid)|

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
	BirthCertificateMenu((Birth Certificate Menu))
	ListPage{Birth Certificate List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    TrackPage((Track Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->BirthCertificateMenu
    subgraph Menu
    BirthCertificateMenu
	end
	subgraph List
	BirthCertificateMenu-->ListPage
	ListPage--C-U-R-V-T-E-->ListPage
	end
	subgraph Error
	BirthCertificateMenu-->ErrorPage
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
|C-U-R-V-E|Create or Update or Remove or View or Track or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant BirthCertificateListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/ctx/BirthCertificate/list ListPage
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S:  GET /app/ctx/BirthCertificate/list ListPage
        cloud-->>-BirthCertificateListPage: RES: List Page
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/create/form CreateFormPage
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/create/form CreateFormPage
        cloud-->>-BirthCertificateListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, POST /app/BirthCertificate/create Create
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : POST /app/BirthCertificate/create Create
        cloud-->>-BirthCertificateListPage: RES: An Birth Certificate Successfully Created
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/update/form UpdateFormPage
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/update/form UpdateFormPage
        cloud-->>-BirthCertificateListPage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, POST /app/BirthCertificate/update update
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : POST /app/BirthCertificate/update Update
        cloud-->>-BirthCertificateListPage: RES: An Birth Certificate Successfully Updated
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/remove/form RemoveFormPage
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/remove/form RemoveFormPage
        cloud-->>-BirthCertificateListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, POST /app/BirthCertificate/remove Remove
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : POST /app/BirthCertificate/remove Remove
        cloud-->>-BirthCertificateListPage: RES: An Birth Certificate Successfully Removed
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/track/form TrackFormPage
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/track/form TrackFormPage
        cloud-->>-BirthCertificateListPage: RES : Track Form Loaded
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, POST /app/BirthCertificate/track Track
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : POST /app/BirthCertificate/track Track
        cloud-->>-BirthCertificateListPage: RES: Birth certificate Object
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/view ViewPage
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/view ViewPage
        cloud-->>-BirthCertificateListPage: RES: birthCertificate View
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/exportPdf ExportPdf
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/exportPdf ExportPdf
        cloud-->>-BirthCertificateListPage: RES: birthCertificate Pdf
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/exportListPdf ExportListPdf
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/exportListPdf ExportListPdf
        cloud-->>-BirthCertificateListPage: RES: birthCertificate List Pdf
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/exportXlx ExportXlx
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/exportXlx ExportXlx
        cloud-->>-BirthCertificateListPage: RES: birthCertificate Xlx
    end
    rect rgb(244,244,244)
        BirthCertificateListPage->>+Net: Check Internet, GET /app/BirthCertificate/exportListXlx ExportListXlx
        Net--x-BirthCertificateListPage: F : Connection Error
        BirthCertificateListPage->>+cloud: S : GET /app/BirthCertificate/exportListXlx ExportListXlx
        cloud-->>-BirthCertificateListPage: RES: birthCertificate List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|1.0|ut_p_c_birthCert_ideal ||
|1.0|ut_p_c_birthCert_input_validate||
|1.0|ut_n_c_birthCert_input_validate||
|1.0|ut_p_c_birthCert_captcha||
|1.0|ut_n_c_birthCert_captcha||
|1.0|ut_p_c_birthCert_father_aid||
|1.0|ut_n_c_birthCert_father_aid||
|1.0|ut_p_c_birthCert_mother_aid||
|1.0|ut_n_c_birthCert_mother_aid||
|1.0|ut_p_c_birthCert_applicant_aid||
|1.0|ut_n_c_birthCert_applicant_aid||
|1.0|ut_p_u_birthCert_ideal ||
|1.0|ut_p_u_birthCert_input_validate||
|1.0|ut_n_u_birthCert_input_validate||
|1.0|ut_p_u_birthCert_captcha||
|1.0|ut_n_u_birthCert_captcha||
|1.0|ut_p_r_birthCert_ideal ||
|1.0|ut_p_r_birthCert_input_validate||
|1.0|ut_n_r_birthCert_input_validate||
|1.0|ut_p_r_birthCert_captcha||
|1.0|ut_n_r_birthCert_captcha||
|1.0|ut_p_t_birthCert_ideal ||
|1.0|ut_p_t_birthCert_captcha||
|1.0|ut_n_t_birthCert_captcha||

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Birth Certificate should be provided in the User Manual.

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




 
