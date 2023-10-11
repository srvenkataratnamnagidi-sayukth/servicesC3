---
title: Property Valuation Certificate
tags : ["Composing"]
---

## Introduction
Property valuation certificate is one of the features of the software product. The property valuation feature provides the service of applying for the property valuation report. One application number will be assigned to each property valuation application. Property valuation application status can be tracked using the application number.

## Business Assumptions
Property valuation feature should be planned at the design phase and updates to the property valuation at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Property valuation feature only accessible at the panchayat level.
1. While creating property valuation, applicant information will be stored.
1. Property owner aadhaar number is required to create the property valuation certificate.

### Non-functional Requirements
1. Property valuation certificate should be tracked using Application Number or Applicant AadhaarId or Application Mobile Number.

### Problem Statement
1. Property valuation feature is required to provide the service of applying for a certificate that shows the worth of a property/asset as on a particular date.

### Design 
1. Each property valuation certificate has a property owner aadhar number, geo id, and applicant information.
1. We can Create, Update, View, Track, and Remove the property valuation certificate.
1. Property valuation certificate status should be changed through the update feature. And it's status should be monitored through the Track feature.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|[gs0006-citizens]({{< ref "gs0006-citizens" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_property_valuation_list|To view all the property valuation certificate|
|uc_property_valuation_search|To search the property valuation certificate|
|uc_property_valuation_create|To create the property valuation certificate|
|uc_property_valuation_update|To update the property valuation certificate|
|uc_property_valuation_remove|To remove the property valuation certificate|
|uc_property_valuation_view|To view the property valuation certificate|
|uc_property_valuation_track|To track the property valuation certificate|
|uc_property_valuation_export|To export the property valuation certificate in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|Track|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|propertyOwnerAid|YES|NA|Allowed 0-9 and length should be 12 Digits|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "property_owner_aid", referencedColumnName = "aid")|property_owner_aid varchar(12) NOT NULL|YES|NO|YES|YES|NO|YES|YES||
|geoid|YES|NA|Allowed a-z = A-Z = 0-9 = . = , and length 3 to 64|@Column(name = "geoid", length = 64, nullable = false, unique = true)|geoid varchar(64) not null|YES|NO|YES|YES|NO|YES|YES||
|applicantAid|YES|NA|0-9|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "applicant_aid", referencedColumnName = "aid")|applicant_aid varchar(12) DEFAULT NULL|YES|NO|YES|YES|YES|YES|YES||
|applicatName|YES|NA|a-zA-Z0-9_/ -.,minlen=3, maxlen=64|@Column(name = "applicat_name", length = 64, nullable = false)|applicat_name varchar(64) NOT NULL|YES|NO|YES|YES|NO|YES|YES||
|applicantSurname|YES|NA|a-zA-Z0-9. _-, minlen=1, maxlen=32|@Column(name = "applicant_surname", length = 32, nullable = false)|applicant_surname varchar(32) NOT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantFSname|YES|NA|a-zA-Z0-9_/ -.,minlen=3, maxlen=64|@Column(name = "applicant_fsname", length = 64, nullable = false)|applicant_fsname varchar(64) NOT NULL|YES|NO|YES|YES|NO|NO|NO||
|applicantMobile|YES|NA|0-9|@Column(name = "applicant_mobile", length = 13, nullable = false)|applicant_mobile varchar(13) NOT NULL|YES|NO|YES|YES|YES|YES|YES||
|applicantEmail|YES|NA|a-zA-Z0-9._@|@Column(name = "applicant_email", length = 64, nullable = true, unique = true)|applicant_email varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|YES|NO||
|applicationNumber|NO|NA|a-zA-Z0-9._@|@Column(name = "application_number", length = 32, nullable = false)|application_number varchar(32) NOT NULL|NO|NO|NO|YES|YES|NO|YES||
|copyNo|YES|NA|Drop Down Values|@Column(name = "copy_no", nullable = true)|copy_no bigint(20) DEFAULT NULL|YES|NO|YES|YES|NO|NO|NO||
|status|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "status_type", length = 16, nullable = true)|status_type varchar(16) DEFAULT NULL|YES|YES|YES|YES|NO|NO|YES||
|descr|YES|NA|a-zA-Z0-9/:#, _.-[]()@|@Column(name = "descr", length = 256, nullable = true)|descr varchar(256) DEFAULT NULL|NO|YES|YES|YES|NO|NO|NO||
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
|Unique Keys|gs_citizenCert__geoid (geoid)|
|Foreign Keys|1. fk__gs_citizenCert__property_owner_aid FOREIGN KEY (property_owner_aid) REFERENCES gs_citizen (aid)|
||2. fk__gs_citizenCert__applicant_aid FOREIGN KEY (applicant_aid) REFERENCES gs_citizen (aid)|

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
	PropertyValuationCertificateMenu((Property Valuation Certificate Menu))
	ListPage{Property Valuation Certificate List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    TrackPage((Track Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->PropertyValuationCertificateMenu
    subgraph Menu
    PropertyValuationCertificateMenu
	end
	subgraph List
	PropertyValuationCertificateMenu-->ListPage
	ListPage--C-U-R-V-T-E-->ListPage
	end
	subgraph Error
	PropertyValuationCertificateMenu-->ErrorPage
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
    participant PropertyValuationCertificateListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/ctx/PropertyValuationCertificate/list ListPage
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S:  GET /app/ctx/PropertyValuationCertificate/list ListPage
        cloud-->>-PropertyValuationCertificateListPage: RES: List Page
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/create/form CreateFormPage
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/create/form CreateFormPage
        cloud-->>-PropertyValuationCertificateListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, POST /app/PropertyValuationCertificate/create Create
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : POST /app/PropertyValuationCertificate/create Create
        cloud-->>-PropertyValuationCertificateListPage: RES: An Property Valuation Successfully Created
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/update/form UpdateFormPage
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/update/form UpdateFormPage
        cloud-->>-PropertyValuationCertificateListPage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, POST /app/PropertyValuationCertificate/update update
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : POST /app/PropertyValuationCertificate/update Update
        cloud-->>-PropertyValuationCertificateListPage: RES: An Property Valuation Successfully Updated
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/remove/form RemoveFormPage
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/remove/form RemoveFormPage
        cloud-->>-PropertyValuationCertificateListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, POST /app/PropertyValuationCertificate/remove Remove
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : POST /app/PropertyValuationCertificate/remove Remove
        cloud-->>-PropertyValuationCertificateListPage: RES: An Property Valuation Successfully Removed
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/track/form TrackFormPage
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/track/form TrackFormPage
        cloud-->>-PropertyValuationCertificateListPage: RES : Track Form Loaded
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, POST /app/PropertyValuationCertificate/track Track
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : POST /app/PropertyValuationCertificate/track Track
        cloud-->>-PropertyValuationCertificateListPage: RES: Property Valuation Object
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/view ViewPage
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/view ViewPage
        cloud-->>-PropertyValuationCertificateListPage: RES: propertyValuationCertificate View
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/exportPdf ExportPdf
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/exportPdf ExportPdf
        cloud-->>-PropertyValuationCertificateListPage: RES: propertyValuationCertificate Pdf
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/exportListPdf ExportListPdf
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/exportListPdf ExportListPdf
        cloud-->>-PropertyValuationCertificateListPage: RES: propertyValuationCertificate List Pdf
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/exportXlx ExportXlx
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/exportXlx ExportXlx
        cloud-->>-PropertyValuationCertificateListPage: RES: propertyValuationCertificate Xlx
    end
    rect rgb(244,244,244)
        PropertyValuationCertificateListPage->>+Net: Check Internet, GET /app/PropertyValuationCertificate/exportListXlx ExportListXlx
        Net--x-PropertyValuationCertificateListPage: F : Connection Error
        PropertyValuationCertificateListPage->>+cloud: S : GET /app/PropertyValuationCertificate/exportListXlx ExportListXlx
        cloud-->>-PropertyValuationCertificateListPage: RES: propertyValuationCertificate List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|1.0|ut_p_c_propertyValuCert_ideal ||
|1.0|ut_p_c_propertyValuCert_input_validate||
|1.0|ut_n_c_propertyValuCert_input_validate||
|1.0|ut_p_c_propertyValuCert_captcha||
|1.0|ut_n_c_propertyValuCert_captcha||
|1.0|ut_p_c_propertyValuCert_property_owner_aid||
|1.0|ut_n_c_propertyValuCert_property_owner_aid||
|1.0|ut_p_c_propertyValuCert_applicant_aid||
|1.0|ut_n_c_propertyValuCert_applicant_aid||
|1.0|ut_p_u_propertyValuCert_ideal ||
|1.0|ut_p_u_propertyValuCert_input_validate||
|1.0|ut_n_u_propertyValuCert_input_validate||
|1.0|ut_p_u_propertyValuCert_captcha||
|1.0|ut_n_u_propertyValuCert_captcha||
|1.0|ut_p_r_propertyValuCert_ideal ||
|1.0|ut_p_r_propertyValuCert_input_validate||
|1.0|ut_n_r_propertyValuCert_input_validate||
|1.0|ut_p_r_propertyValuCert_captcha||
|1.0|ut_n_r_propertyValuCert_captcha||
|1.0|ut_p_t_propertyValuCert_ideal ||
|1.0|ut_p_t_propertyValuCert_captcha||
|1.0|ut_n_t_propertyValuCert_captcha||

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Property Valuation Certificate should be provided in the User Manual.

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




 
