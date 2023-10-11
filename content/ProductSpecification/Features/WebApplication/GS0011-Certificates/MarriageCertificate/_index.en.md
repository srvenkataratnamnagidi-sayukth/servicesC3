---
title: Marriage Certificate
tags : ["Composing"]
---

## Introduction
Marriage Certificate is one of the basic features of the software product. Marriage Certificate feature provides the service of applying for the marriage certificate. One application number will be assigned to the each marriage certificate application. Marriage certificate application status can be tracked using application number.

## Business Assumptions
Marriage Certificate Feature should be planned at the design phase and updates to the marriage certificate at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Marriage Certificate feature is only accessible at the panchayat level.
1. While creating marriage certificate, applicant information will be stored.

### Non-functional Requirements
1. Marriage certificate should be tracked using Application Number or Applicant AadhaarId or Application Mobile Number.

### Problem Statement
1. Marriage certificate feature is required to provide the service of applying for marriage certificate.

### Design 
1. Each Marriage certificate has Bridegroom Information, Bride Information, Witness Information, and Applicant Information.
1. We can Create, Update, View, Track, and Remove the Marriage Certificate.
1. Marriage certificate status should be changed through update feature. And it's status should be monitored through Track feature.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|[gs0006-citizens]({{< ref "gs0006-citizens" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_marriage_certificate_list|To view all the marriage certificates|
|uc_marriage_certificate_search|To search the marriage certificate|
|uc_marriage_certificate_create|To create the marriage certificate|
|uc_marriage_certificate_update|To update the marriage certificate|
|uc_marriage_certificate_remove|To remove the marriage certificate|
|uc_marriage_certificate_view|To view the marriage certificate|
|uc_marriage_certificate_track|To track the marriage certificate|
|uc_marriage_certificate_export|To export the marriage certificate in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|Track|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|brideGroomAid|YES|NA|0-9, maxlen=12|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "bridegroom_aid", referencedColumnName = "aid")|bridegroom_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|brideGroomFatherAid|YES|NA|0-9, maxlen=12|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "bridegroom_father_aid", referencedColumnName = "aid")|bridegroom_father_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|NO||
|brideAid|YES|NA|0-9, maxlen=12|@Column(name = "bride_aid", length = 12, nullable = true)|bride_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|brideFatherAid|YES|NA|0-9, maxlen=12|@Column(name = "bride_father_aid", length = 12, nullable = true)|bride_father_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|YES|NO||
|marriageDate|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "marriage_date", nullable = false)|marriage_date datetime DEFAULT NULL|YES|NO|YES|YES|NO|YES|YES||
|witness1Aid|YES|NA|0-9, maxlen=12|@Column(name = "witness1_aid", length = 12, nullable = true)|witness1_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|witness1Name|YES|NA|a-zA-Z0-9. _-, minlen=3, maxlen=64|@Column(name = "witness1_name", length = 64, nullable = true)|witness1_name varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|witness1Mobile|YES|NA|0-9, maxlen=10|@Column(name = "witness1_mobile", length = 13, nullable = true)|witness1_mobile varchar(13) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|witness2Aid|YES|NA|0-9, maxlen=12|@Column(name = "witness2_aid", length = 12, nullable = true)|witness2_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|witness2Name|YES|NA|a-zA-Z0-9. _-, minlen=3, maxlen=64|@Column(name = "witness2_name", length = 64, nullable = true)|witness2_name varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|witness2Mobile|YES|NA|0-9, maxlen=10|@Column(name = "witness2_mobile", length = 13, nullable = true)|witness2_mobile varchar(13) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
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
|Foreign Keys|1. fk__gs_citizenCert__bridegroom_aid FOREIGN KEY (bridegroom_aid) REFERENCES gs_citizen (aid)|
||2. fk__gs_citizenCert__bridegroom_father_aid FOREIGN KEY (bridegroom_father_aid) REFERENCES gs_citizen (aid)|
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
	MarriageCertificateMenu((Marriage Certificate Menu))
	ListPage{Marriage Certificate List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    TrackPage((Track Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->MarriageCertificateMenu
    subgraph Menu
    MarriageCertificateMenu
	end
	subgraph List
	MarriageCertificateMenu-->ListPage
	ListPage--C-U-R-V-T-E-->ListPage
	end
	subgraph Error
	MarriageCertificateMenu-->ErrorPage
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
    participant MarriageCertificateListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/ctx/MarriageCertificate/list ListPage
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S:  GET /app/ctx/MarriageCertificate/list ListPage
        cloud-->>-MarriageCertificateListPage: RES: List Page
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/create/form CreateFormPage
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/create/form CreateFormPage
        cloud-->>-MarriageCertificateListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, POST /app/MarriageCertificate/create Create
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : POST /app/MarriageCertificate/create Create
        cloud-->>-MarriageCertificateListPage: RES: An Marriage Certificate Successfully Created
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/update/form UpdateFormPage
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/update/form UpdateFormPage
        cloud-->>-MarriageCertificateListPage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, POST /app/MarriageCertificate/update update
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : POST /app/MarriageCertificate/update Update
        cloud-->>-MarriageCertificateListPage: RES: An Marriage Certificate Successfully Updated
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/remove/form RemoveFormPage
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/remove/form RemoveFormPage
        cloud-->>-MarriageCertificateListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, POST /app/MarriageCertificate/remove Remove
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : POST /app/MarriageCertificate/remove Remove
        cloud-->>-MarriageCertificateListPage: RES: An Marriage Certificate Successfully Removed
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/track/form TrackFormPage
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/track/form TrackFormPage
        cloud-->>-MarriageCertificateListPage: RES : Track Form Loaded
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, POST /app/MarriageCertificate/track Track
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : POST /app/MarriageCertificate/track Track
        cloud-->>-MarriageCertificateListPage: RES: Marriage certificate Object
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/view ViewPage
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/view ViewPage
        cloud-->>-MarriageCertificateListPage: RES: marriageCertificate View
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/exportPdf ExportPdf
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/exportPdf ExportPdf
        cloud-->>-MarriageCertificateListPage: RES: marriageCertificate Pdf
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/exportListPdf ExportListPdf
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/exportListPdf ExportListPdf
        cloud-->>-MarriageCertificateListPage: RES: marriageCertificate List Pdf
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/exportXlx ExportXlx
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/exportXlx ExportXlx
        cloud-->>-MarriageCertificateListPage: RES: marriageCertificate Xlx
    end
    rect rgb(244,244,244)
        MarriageCertificateListPage->>+Net: Check Internet, GET /app/MarriageCertificate/exportListXlx ExportListXlx
        Net--x-MarriageCertificateListPage: F : Connection Error
        MarriageCertificateListPage->>+cloud: S : GET /app/MarriageCertificate/exportListXlx ExportListXlx
        cloud-->>-MarriageCertificateListPage: RES: marriageCertificate List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|1.0|ut_p_c_marriageCert_ideal ||
|1.0|ut_p_c_marriageCert_input_validate||
|1.0|ut_n_c_marriageCert_input_validate||
|1.0|ut_p_c_marriageCert_captcha||
|1.0|ut_n_c_marriageCert_captcha||
|1.0|ut_p_c_marriageCert_bride_groom_aid||
|1.0|ut_n_c_marriageCert_bride_groom_father_aid||
|1.0|ut_p_c_marriageCert_applicant_aid||
|1.0|ut_n_c_marriageCert_applicant_aid||
|1.0|ut_p_u_marriageCert_ideal ||
|1.0|ut_p_u_marriageCert_input_validate||
|1.0|ut_n_u_marriageCert_input_validate||
|1.0|ut_p_u_marriageCert_captcha||
|1.0|ut_n_u_marriageCert_captcha||
|1.0|ut_p_r_marriageCert_ideal ||
|1.0|ut_p_r_marriageCert_input_validate||
|1.0|ut_n_r_marriageCert_input_validate||
|1.0|ut_p_r_marriageCert_captcha||
|1.0|ut_n_r_marriageCert_captcha||
|1.0|ut_p_t_marriageCert_ideal ||
|1.0|ut_p_t_marriageCert_captcha||
|1.0|ut_n_t_marriageCert_captcha||

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Marriage Certificate should be provided in the User Manual.

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




 
