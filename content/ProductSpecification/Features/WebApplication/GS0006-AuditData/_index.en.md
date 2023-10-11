---
title: GS0006 - Audit Data
tags : ["Composing"]
---

## Introduction
Audit data is one of the basic features of the software product. Audit data feature will show all the operations performed in various features of our product by logged in users. Users should have permission to access this feature. 

## Business Assumptions
Audit data should be planned at the design phase and no updates to audit data at the run time.

## Requirements
### Functional Requirements
1. The audit data feature is accessible at all levels of the organization.
1. Audit data is created when operations like create, update, remove, export, etc are performed on any feature of the product.

## Non-functional Requirements
Audit data feature has view and export features only.

### Problem Statement
Audit data is required to export and view the operations performed on any features of the product.

### Design 
1. We can view and export the audit data.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|TaxableProperties|[gs0006-taxableProperties]({{< ref "gs0006-taxableProperties" >}})||
|Citizens|[gs0006-citizens]({{< ref "gs0006-citizens" >}})||
|PanchayatAssets|[gs0007-panchayatAssets]({{< ref "gs0007-panchayatAssets" >}})||
|Grievances|[gs0007-grievances]({{< ref "gs0007-grievances" >}})||
|Administration|[gs0008-administration]({{< ref "gs0008-administration" >}})||
|Organizations|[gs0009-organizations]({{< ref "gs0009-organizations" >}})||
|UserRoles|[gs0003-userRoles]({{< ref "gs0003-userRoles" >}})||
|User|[gs0004-users]({{< ref "gs0004-users" >}})||
|SurveyUser|[gs0010-surveyUser]({{< ref "gs0010-surveyUser" >}})||
|Certificates|[gs0011-certificates]({{< ref "gs0011-certificates" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_audit_data_view|To view the audit data |
|uc_audit_data_export|To export the audit data in 2 formats Excel, PDF.|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|Operation|YES|NA|Drop Down List|@Enumerated(EnumType.STRING)@Column(name = "operation", length = 24, nullable = false)|operation varchar(24) NOT NULL|NO|NO|NO|YES|YES|YES||
|Class|YES|NA|Allowed a-z , A-Z and length 3 to 32|@Column(name = "clazz", length = 32, nullable = false)|clazz varchar(32) NOT NULL|NO|NO|NO|YES|YES|YES||
|Remote IP|YES|NA|Allowed 0-9 , . and length must be 15|@Column(name = "remote_ip", length = 16, nullable = true) |remote_ip varchar(16) DEFAULT NULL|NO|NO|NO|YES|YES|YES||
|Session Id|YES|NA|NA|@Column(name = "session_id", length = 36, nullable = true)|session_id varchar(36) DEFAULT NULL|NO|NO|NO|YES|YES|NO||
|Object Id|YES|NA|Allowed only 0-9 and -|@Column(name = "obj_id", length = 36, nullable = true)|obj_id varchar(36) DEFAULT NULL|NO|NO|NO|YES|YES|YES||

#### ENUM CONSTANTS

##### Operation

{{<mermaid align="left">}}
classDiagram
    class Name{
      CREATE
      UPDATE
      REMOVE
      DELETE
      EXPORT
      DOWNLOAD
      AUTH_LOGIN
      AUTH_LOGOUT
      AUTH_FAILED
      AUTH_APP_FAILED
	  AUTH_APP_LOGIN
	  AUTH_APP_LOGOUT
	  AUTH_API_LOGIN
	  AUTH_API_LOGOUT
	  AUTH_API_FAILED
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|AUDIT_DATA_VIEW|View |
|AUDIT_DATA_VIEW|Export |

#### Constraints
|Constraint|Key|
|----------|----|
|||

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|ac_audit_data_view|Only user having the permission to view, should view this functionality|
|ac_audit_data_view|Only user having the permission to view, should export the user role in 2 formats Excel, PDF|

## User Experience
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### View Page Buttons
{{<mermaid align="left">}}
graph LR 
    ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	AuditDataMenu((Audit Data Menu))
	ListPage{Audit Data List Page}
    ViewPage((View Page))
    ErrorPage((Error Page))
    DownloadFile>Save File On Disk]
    Stop((Stop))
	Start((Start))
	Start-->AuditDataMenu
	subgraph Menu
	AuditDataMenu
	end
	subgraph List
	AuditDataMenu-->ListPage
	ListPage--VE-->ListPage
	end
	subgraph Error
	AuditDataMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--B-->ListPage
	ViewPage--B-->ViewPage
	end
	subgraph Download
	ListPage--E-->DownloadFile
	end
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 3 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
	linkStyle 7 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|V|View|
|E|Export|
|VE|View or Export|
|B|Back|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant AuditDataListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AuditDataListPage->>+Net: Check Internet, GET /app/ctx/AuditData/list ListPage
        Net--x-AuditDataListPage: F : Connection Error
        AuditDataListPage->>+cloud: S:  GET /app/ctx/AuditData/list ListPage
        cloud-->>-AuditDataListPage: RES:List Page
    end
    rect rgb(244,244,244)
        AuditDataListPage->>+Net: Check Internet, GET /app/AuditData/view ViewPage
        Net--x-AuditDataListPage: F : Connection Error
        AuditDataListPage->>+cloud: S : GET /app/AuditData/view ViewPage
        cloud-->>-AuditDataListPage: RES: Audit Data View
    end
    rect rgb(244,244,244)
        AuditDataListPage->>+Net: Check Internet, GET /app/AuditData/exportPdf ExportPdf
        Net--x-AuditDataListPage: F : Connection Error
        AuditDataListPage->>+cloud: S : GET /app/AuditData/exportPdf ExportPdf
        cloud-->>-AuditDataListPage: RES: auditData Pdf
    end
    rect rgb(244,244,244)
        AuditDataListPage->>+Net: Check Internet, GET /app/AuditData/exportListPdf ExportListPdf
        Net--x-AuditDataListPage: F : Connection Error
        AuditDataListPage->>+cloud: S : GET /app/AuditData/exportListPdf ExportListPdf
        cloud-->>-AuditDataListPage: RES: auditData List Pdf
    end
    rect rgb(244,244,244)
        AuditDataListPage->>+Net: Check Internet, GET /app/AuditData/exportXlx ExportXlx
        Net--x-AuditDataListPage: F : Connection Error
        AuditDataListPage->>+cloud: S : GET /app/AuditData/exportXlx ExportXlx
        cloud-->>-AuditDataListPage: RES: auditData Xlx
    end
    rect rgb(244,244,244)
        AuditDataListPage->>+Net: Check Internet, GET /app/AuditData/exportListXlx ExportListXlx
        Net--x-AuditDataListPage: F : Connection Error
        AuditDataListPage->>+cloud: S : GET /app/AuditData/exportListXlx ExportListXlx
        cloud-->>-AuditDataListPage: RES: auditData List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
||||

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Audit Data in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
