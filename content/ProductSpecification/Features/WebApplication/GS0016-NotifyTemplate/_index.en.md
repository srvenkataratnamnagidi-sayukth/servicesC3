---
title: GS0016 - Notify Template
tags : ["Composing"]
---

## Introduction
Notify Template is one of the features of our software product. Notify template holds various notification messages which were sent to the user. The notification message which is sent to the user is verified by the government and assigns a registration Id for every message. Users should have permission to access this feature.

## Business Assumptions
Creating, updating, and removing the notify template can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
1. The notify template feature is accessible at all levels of the organization.
1. Each notify template has a unique code and registration Id.

### Non-functional Requirements
Permission for accessing this feature should only be given to the admin.

### Problem Statement
Notify template is required to save the notification messages which are needed to be sent to the user.

### Design 
1. Each Notify template has a notify type, code, registration Id, short note, and full note.
1. We can Create, Update, View, and remove the notify template.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_notify_template_create|To create the notify template|
|uc_notify_template_update|To update the notify template|
|uc_notify_template_remove|To remove the notify template|
|uc_notify_template_view|To view the notify template|
|uc_notify_template_list|To view all the notify template|
|uc_notify_template_search|To search the notify template|
|uc_notify_template_export|To export the notify template in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|type|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "notify_type", length = 15, nullable = false)|notify_type varchar(15) not null|YES|NO|YES|YES|YES|YES||
|code|YES|NA|Allowed a-z, A-Z|@Column(name = "code", length = 32, nullable = false|code varchar(32) not null|YES|NO|YES|YES|YES|YES||
|regId|NO|NA|Allowed a-z, A-Z, 0-9|@Column(name = "reg_Id", length = 31, nullable = true)|reg_id varchar(31) default null|YES|YES|YES|YES|YES|NO||
|shortNote|YES|NA|Allowed a-z, A-Z, 0-9, space, $, @, %, &, *, =, ;, ., #, :, _, -, {, }, [, ], (, ), +, ', <, >, \, ", and ,|@Column(name = "short_note", length = 255, nullable = false)|short_note varchar(255) not null|YES|YES|YES|YES|YES|NO||
|fullNote|NO|NA|Allowed a-z, A-Z, 0-9, space, $, @, %, &, *, =, ;, ., #, :, _, -, {, }, [, ], (, ), +, ', <, >, \, ", and ,|@Column(name = "full_note", length = 1023, nullable = true)|full_note varchar(1023) default null|YES|YES|YES|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Notify Type

{{<mermaid align="left">}}
classDiagram
    class OrgType{
      SMS
      EMAIL 
      WHATSAPP
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|NOTIFY_TEMPLATE_CREATE|Create|
|NOTIFY_TEMPLATE_UPDATE|Update|
|NOTIFY_TEMPLATE_REMOVE|Remove|
|NOTIFY_TEMPLATE_VIEW|View|
|NOTIFY_TEMPLATE_VIEW|List|
|NOTIFY_TEMPLATE_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_notify_template__code__notify_type (code,notify_type)|
||uk__gs_notify_template__reg_Id (reg_Id)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|AC_ROLE_NOTIFY_TEMPLATE_CREATE|Only user having the permission to create, should create this functionality|
|AC_ROLE_NOTIFY_TEMPLATE_UPDATE|Only user having the permission to update, should update this functionality|
|AC_ROLE_NOTIFY_TEMPLATE_REMOVE|Only user having the permission to remove, should remove this functionality|
|AC_ROLE_NOTIFY_TEMPLATE_VIEW|Only user having the permission to view, should view this functionality|
|AC_ROLE_NOTIFY_TEMPLATE_VIEW|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|
## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreteBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	NotifyTemplateMenu((Notify Template Menu))
	ListPage{Notify Template List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->NotifyTemplateMenu
    subgraph Menu
    NotifyTemplateMenu
	end
	subgraph List
	NotifyTemplateMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	NotifyTemplateMenu-->ErrorPage
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
	ViewPage--SB-->ListPage
	ViewPage--SB-->ViewPage
	end
	subgraph Remove
	ListPage--R-->RemovePage
	RemovePage--SB-->ListPage
	RemovePage--SB-->RemovePage
	end
	subgraph Download
    ListPage--E-->DownloadFile
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
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
	
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
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-V-E|Create or Update or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram
1. Only a user with the NOTIFY_TEMPLATE_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant NotifyTemplateListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet, GET /app/ctx/NotifyTemplate/list ListPage
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S:  GET /app/ctx/NotifyTemplate/list ListPage
        cloud-->>-NotifyTemplateListPage: RES:List Page
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet, GET /app/NotifyTemplate/create/form CreateFormPage
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : GET /app/NotifyTemplate/create/form CreateFormPage
        cloud-->>-NotifyTemplateListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: POST /app/NotifyTemplate/create Create
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : POST /app/NotifyTemplate/create Create
        cloud-->>-NotifyTemplateListPage: RES: An NOTIFY Template Successfully Created
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/update/form UpdateFormPage
        Net--x-NotifyTemplateListPage: F : Connection Error
        alt
        note right of Net:  NotifyTemplate Cache Object Found
        NotifyTemplateListPage->>+Cache: S : GET /app/NotifyTemplate/update/form UpdateFormPage
        Cache-->>-NotifyTemplateListPage: RES: Update Form Loaded
        else
		note right of Net:  NotifyTemplate Cache Object Not Found
        Cache->>+cloud: GET /app/NotifyTemplate/update/form UpdateFormPage
        cloud-->>-NotifyTemplateListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: POST /app/NotifyTemplate/update update
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : POST /app/NotifyTemplate/update Update
        cloud-->>-NotifyTemplateListPage: RES: An Notify Template Successfully Updated
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/remove/form RemoveFormPage
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : GET /app/NotifyTemplate/remove/form RemoveFormPage
        cloud-->>-NotifyTemplateListPage: Response : Remove Form Loaded
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: POST /app/NotifyTemplate/remove Remove
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : POST /app/NotifyTemplate/remove Remove
        cloud-->>-NotifyTemplateListPage: RES: An Notify Template Successfully Removed
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/view ViewPage
        Net--x-NotifyTemplateListPage: F : Connection Error
        alt
		note right of Net:  NotifyTemplate Cache Object Found
        NotifyTemplateListPage->>+Cache: S : GET /app/NotifyTemplate/view ViewPage
        Cache-->>-NotifyTemplateListPage: RES: notifyTemplate View
        else
		note right of Net:  NotifyTemplate Cache Object Not Found
        Cache->>+cloud: GET /app/NotifyTemplate/view ViewPage
        cloud-->>-NotifyTemplateListPage: RES: notifyTemplate View
        end
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/exportPdf ExportPdf
        Net--x-NotifyTemplateListPage: F : Connection Error
        alt
		note right of Net:  NotifyTemplate Cache Object Found
        NotifyTemplateListPage->>+Cache: S : GET /app/NotifyTemplate/exportPdf ExportPdf
        Cache-->>-NotifyTemplateListPage: RES: notifyTemplate Pdf
        else
		note right of Net:  NotifyTemplate Cache Object Not Found
        Cache->>+cloud: GET /app/NotifyTemplate/exportPdf ExportPdf
        cloud-->>-NotifyTemplateListPage: RES: notifyTemplate Pdf
        end
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/exportListPdf ExportListPdf
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : GET /app/NotifyTemplate/exportListPdf ExportListPdf
        cloud-->>-NotifyTemplateListPage: RES: notifyTemplate List Pdf
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/exportXlx ExportXlx
        Net--x-NotifyTemplateListPage: F : Connection Error
        alt
		note right of Net:  NotifyTemplate Cache Object Found
        NotifyTemplateListPage->>+Cache: S : GET /app/NotifyTemplate/exportXlx ExportXlx
        Cache-->>-NotifyTemplateListPage: RES: notifyTemplate Xlx
        else
		note right of Net:  NotifyTemplate Cache Object Not Found
        Cache->>+cloud: GET /app/NotifyTemplate/exportXlx ExportXlx
        cloud-->>-NotifyTemplateListPage: RES: notifyTemplate Xlx
        end
    end
    rect rgb(244,244,244)
        NotifyTemplateListPage->>+Net: Check Internet: GET /app/NotifyTemplate/exportListXlx ExportListXlx
        Net--x-NotifyTemplateListPage: F : Connection Error
        NotifyTemplateListPage->>+cloud: S : GET /app/NotifyTemplate/exportListXlx ExportListXlx
        cloud-->>-NotifyTemplateListPage: RES: notifyTemplate List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|1.0|ut_p_c_notifyTemplate_ideal||
|1.0|ut_p_c_notifyTemplate_captcha||
|1.0|ut_n_c_notifyTemplate_captcha||
|1.0|ut_p_u_notifyTemplate_ideal||
.0|ut_p_u_notifyTemplate_captcha||
|1.0|ut_n_u_notifyTemplate_captcha||
|1.0|ut_p_r_notifyTemplate_ideal||
1.0|ut_p_r_notifyTemplate_captcha||
|1.0|ut_n_r_notifyTemplate_captcha||

## Security compliance check
1. Only user having the notify template with permission **ROLE_NOTIFY_TEMPLATE_CREATE** should create this functionality 
1. Only user having the notify template with permission **ROLE_NOTIFY_TEMPLATE_UPDATE** should update this functionality 
1. Only user having the notify template with permission **ROLE_NOTIFY_TEMPLATE_REMOVE** should remove this functionality 
1. Only user having the notify template with permission **ROLE_NOTIFY_TEMPLATE_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the NOTIFY TEMPLATE in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
