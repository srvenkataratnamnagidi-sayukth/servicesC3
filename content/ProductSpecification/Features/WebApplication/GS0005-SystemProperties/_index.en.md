---
title: GS0005 - System Properties
tags : ["Composing"]
---

## Introduction
System Properties are one of the basic building blocks of the software product. System Properties includes the information of properties of the product like product URL, product name, product logo.

## Business Assumptions
System Properties should be planned at the design phase and no updates to the properties at the run time. Only the administrator will have access to view or export these system properties.

## Requirements
### Functional Requirements
In system properties, each property should have a name that has to be unique.

### Non-functional Requirements
System can support any number of properties but this design will limit 1000 properties for this system. Beyond the 1000 properties of the system may experience performance issues. 

### Problem Statement
System properties are required to provide some fixed information about the product.

### Design 
1. Each system property have name, value and description. Name give to each system property should be unique.
1. Insert the system properties in the Database directly. We should not have options to Create and Update the system property.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_system_property_view|To view the system property. This listing page should bind to a permission|
|uc_system_property_export|To export the system property in 2 formats Excel, PDF. This export page should bind a permission|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9 space - _ , maxlength=64|@Column(name = "name", length = 64, nullable = false, unique = true)|name varchar(64) not null uk__gs_user_permission__name (name)|-|-|-|YES|YES|YES||
|value|YES|NA|a-zA-Z0-9 space - _ , maxlength=32|@Column(name = "value", length = 32, nullable = false)|value varchar(32) not null|-|-|-|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9 space - _ , maxlength=128|@Column(name = "descr", length = 128, nullable = false)|descr varchar(128) not null|-|-|-|YES|YES|YES||

#### Feature Permission


|Permission code|Action|
|---------------|-------|
|SYSTEM_PROPERTY_VIEW|View|
|SYSTEM_PROPERTY_VIEW|List|
|SYSTEM_PROPERTY_VIEW|Export|

## Acceptance Criteria
|Acceptance Criteria|Description|
|-------------------|-----------|
|ac_system_property_view|To view the system property. This listing page should bind to a permission|

## User Experience
### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
graph TD 
	SystemPropertiesMenu((System Properties Menu))
	ListPage{System Properties List Page}
	ViewPage((ViewPage))
	DownloadFile>Save File On Disk]
	ErrorPage((ErrorPage))
	Stop((Stop))
	Start((Start))
	Start-->SystemPropertiesMenu
	subgraph Menu
    SystemPropertiesMenu
	end
	subgraph List
	SystemPropertiesMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	SystemPropertiesMenu-->ErrorPage
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
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px; 
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;   
{{< /mermaid >}}



|Symbol|Action|
|:-----|:-----|
|V|View|
|E|Export|
|B|Back|
|V-E|View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram
{{<mermaid align="center">}}
sequenceDiagram
    participant SystemPropertiesListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        SystemPropertiesListPage->>+Net: Check Internet, GET /app/ctx/SystemProperty/list ListPage
        Net--x-SystemPropertiesListPage: F : Connection Error
        SystemPropertiesListPage->>+cloud: S:  GET /app/ctx/SystemProperty/list ListPage
        cloud-->>-SystemPropertiesListPage: RES:List Page
    end
    rect rgb(244,244,244)
        SystemPropertiesListPage->>+Net: Check Internet: GET /app/SystemProperty/view ViewPage
        Net--x-SystemPropertiesListPage: F : Connection Error
        alt 
        Note right of Net: System Property Cache Object Found
        SystemPropertiesListPage->>+Cache: S : GET /app/SystemProperty/view ViewPage
        Cache-->>-SystemPropertiesListPage: RES: systemProperty View
        else  
        Note right of Net: System Property Cache Object Not Found
        Cache->>+cloud: GET /app/SystemProperty/view ViewPage
        cloud-->>-SystemPropertiesListPage: RES: systemProperty View
        end
    end
    rect rgb(244,244,244)
        SystemPropertiesListPage->>+Net: Check Internet: GET /app/SystemProperty/exportPdf ExportPdf
        Net--x-SystemPropertiesListPage: F : Connection Error
        alt 
        Note right of Net: System Property Cache Object Found
        SystemPropertiesListPage->>+Cache: S : GET /app/SystemProperty/exportPdf ExportPdf
        Cache-->>-SystemPropertiesListPage: RES: systemProperty Pdf
        else 
        Note right of Net: System Property Cache Object Not Found
        Cache->>+cloud: GET /app/SystemProperty/exportPdf ExportPdf
        cloud-->>-SystemPropertiesListPage: RES: systemProperty Pdf
        end
    end
    rect rgb(244,244,244)
        SystemPropertiesListPage->>+Net: Check Internet: GET /app/SystemProperty/exportListPdf ExportListPdf
        Net--x-SystemPropertiesListPage: F : Connection Error
        SystemPropertiesListPage->>+cloud: S : GET /app/SystemProperty/exportListPdf ExportListPdf
        cloud-->>-SystemPropertiesListPage: RES: systemProperty List Pdf
    end
    rect rgb(244,244,244)
        SystemPropertiesListPage->>+Net: Check Internet: GET /app/SystemProperty/exportXlx ExportXlx
        Net--x-SystemPropertiesListPage: F : Connection Error
        alt 
        Note right of Net: System Property Cache Object Found
        SystemPropertiesListPage->>+Cache: S : GET /app/SystemProperty/exportXlx ExportXlx
        Cache-->>-SystemPropertiesListPage: RES: systemProperty Xlx
        else
        Note right of Net: System Property Cache Object Not Found
        Cache->>+cloud: GET /app/SystemProperty/exportXlx ExportXlx
        cloud-->>-SystemPropertiesListPage: RES: systemProperty Xlx
        end
    end
    rect rgb(244,244,244)
        SystemPropertiesListPage->>+Net: Check Internet: GET /app/SystemProperty/exportListXlx ExportListXlx
        Net--x-SystemPropertiesListPage: F : Connection Error
        SystemPropertiesListPage->>+cloud: S : GET /app/SystemProperty/exportListXlx ExportListXlx
        cloud-->>-SystemPropertiesListPage: RES: systemProperty List Xlx
    end
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|---|
|1.0| View |ut_p_v_GSTS_WEB_SYSTEMPROPERTY_100  ut_n_v_GSTS_WEB_SYSTEMPROPERTY_110 ut_n_v_GSTS_WEB_SYSTEMPROPERTY_120 |**Positive Test Cases:** View System Property with Valid Id  with Authorised User **Negative Test Cases:** 1.View System Property without DB Connection 2.View System Property with Invalid ID with Authorised User||1|2|3|testPosSLAuthorisedUserViewSystemPropertyWithValidId,  testNegAuthorisedUserViewSystemPropertyWithoutDbConnection,  testNegAuthorisedUserViewSystemPropertywithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_SYSTEMPROPERTY_170  ut_n_s_GSTS_WEB_SYSTEMPROPERTY_180 ut_n_s_GSTS_WEB_SYSTEMPROPERTY_190 |**Positive Test Cases:** Search System Property with valid inputs **Negative Test Cases:** 1.Search System Property without db connection 2.Search System Property with invalid inputs| **name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>=3 and length=<64  3.null **value:** 1.length<=32 2.null **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null|1|2|3|testPosAuthorisedUserSearchSystemPropertyWithValidInputs, testNegAuthorisedUserSearchSystemPropertyWithoutDBconnection,  testNegAuthorisedUserSearchSystemPropertyWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_SYSTEMPROPERTY_140 ut_n_l_GSTS_WEB_SYSTEMPROPERTY_150|**Positive Test Cases:** Get System Property List **Negative Test Cases:** Get System Property List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserSystemPropertyList,  testNegAuthorisedUserSystemPropertyListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_SYSTEMPROPERTY_360   ut_n_ep_GSTS_WEB_SYSTEMPROPERTY_370   ut_n_ep_GSTS_WEB_SYSTEMPROPERTY_380 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportSystemPropertyPdfWithValidId,  testNegAuthorisedUserExportSystemPropertyPdfwithoutDbConnection,  testNegAuthorisedUserExportSystemPropertyPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_SYSTEMPROPERTY_390   ut_n_elp_GSTS_WEB_SYSTEMPROPERTY_400   ut_n_elp_GSTS_WEB_SYSTEMPROPERTY_410 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportSystemPropertyListPdfWithValidId,  testNegAuthorisedUserExportSystemPropertyListPdfwithoutDbConnection,  testNegAuthorisedUserExportSystemPropertyListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_SYSTEMPROPERTY_420   ut_n_ex_GSTS_WEB_SYSTEMPROPERTY_430   ut_n_ex_GSTS_WEB_SYSTEMPROPERTY_440 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportSystemPropertyXlxValidId,  testNegAuthorisedUserExportSystemPropertyXlxwithoutDbConnection,  testNegAuthorisedUserExportSystemPropertyXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_SYSTEMPROPERTY_450   ut_n_elx_GSTS_WEB_SYSTEMPROPERTY_460   ut_n_elx_GSTS_WEB_SYSTEMPROPERTY_470 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportSystemPropertyListXlxValidId,  testNegAuthorisedUserExportSystemPropertyListXlxWithoutDbConnection,  testNegAuthorisedUserExportSystemPropertyListXlxInValidId|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| View |ut_n_v_GSTS_WEB_SYSTEMPROPERTY_130|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewSystemProperty|
|1.0| Search |ut_n_s_GSTS_WEB_SYSTEMPROPERTY_200|Unauthorised User does not have permission to search| **name:** 1.valid characters 2. length>=3 and length=<64  3.null **value:** 1.length<=32 2.null **descr:** 1.valid characters 2. length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserSearchSystemProperty|
|1.0| List |ut_n_l_GSTS_WEB_SYSTEMPROPERTY_160|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserSystemPropertyList|
|1.0| PDF |ut_n_ep_GSTS_WEB_SYSTEMPROPERTY_510 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportSystemPropertyPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_SYSTEMPROPERTY_520 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportSystemPropertyListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_SYSTEMPROPERTY_530 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportSystemPropertyXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_SYSTEMPROPERTY_540 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportSystemPropertyListXlxWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|

## Security compliance check
1. Only user having the permission **ROLE_SYSTEM_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the SYSTEM PROPERTIES in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
