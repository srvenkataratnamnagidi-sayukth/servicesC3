---
title: GS0025 - Customer Care
tags : ["Composing"]
---

## Introduction
Customer Care is one of the basic features of the software product. By using this feature, Users can contact the support team and clarify his/her doubts.

## Business Assumptions
1. Customer Care feature should be planned at the design phase.
1. List of Customer Care Details are provided in the feature.

## Requirements
### Functional Requirements
1. Customer Care feature is accessible at independent of context.
1. Customer Care feature has name, mobile number, category, register aadhaar, register name, and network.

### Non-functional Requirements
1. Technical team will create the customer care details.
1. User can find the contact details of a support team in this feature.

### Problem Statement
Customer Care feature is required to store all the details of support team.

### Design 
1. Each customer care have name, mobileNumber, category, registerAadhaar, registerName, and network.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_customer_care_create|To create the customer care|
|uc_customer_care_remove|To remove the customer care|
|uc_customer_care_view|To view the customer care. This listing page should bind to a permission|
|uc_customer_care_search|To search the customer care|
|uc_customer_care_export|To export the customer care in 2 formats Excel, PDF. This export page should bind a permission|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9 space - _ , maxlength=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|NA|YES|YES|YES|YES||
|mobileNumber|YES|NA|0-9|@Column(name = "mobile_number", length = 13, nullable = false)|mobile_number varchar(13) NOT NULL|YES|NA|YES|YES|YES|YES||
|category|YES|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "category", length = 14, nullable = false)|category varchar(14) NOT NULL|YES|NA|YES|YES|YES|YES||
|registerAadhaar|YES|NA|Allowed 0-9 and length should be 12|@Column(name = "register_aadhaar", length = 12, nullable = false)|register_aadhaar varchar(12) NOT NULL|YES|NA|YES|YES|YES|YES||
|registerName|YES|NA|a-zA-Z0-9 space - _ , maxlength=64|@Column(name = "register_name", length = 64, nullable = false)|register_name varchar(64) NOT NULL|YES|NA|YES|YES|YES|YES||
|network|YES|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "network", length = 7, nullable = false)|network varchar(7) NOT NULL|YES|NA|YES|YES|YES|YES||

#### ENUM CONSTANTS

##### CustomerCatType

{{<mermaid align="left">}}
classDiagram
    class CustomerCatType{
      CUSTOMER_CARE
      SUPPORT
      NONE
    }
{{< /mermaid >}}

##### NetworkType

{{<mermaid align="left">}}
classDiagram
    class NetworkType{
      BSNL
      AIRTEL
      JIO
      IDEA
    }
{{< /mermaid >}}

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|CUSTOMER_CARE_CREATE|Create|
|CUSTOMER_CARE_REMOVE|Remove|
|CUSTOMER_CARE_VIEW|View|
|CUSTOMER_CARE_VIEW|Search|
|CUSTOMER_CARE_VIEW|Export|

## Acceptance Criteria
|Acceptance Criteria|Description|
|-------------------|-----------|
|ac_customer_care_create|Only user having the permission to create, should create this functionality|
|ac_customer_care_remove|Only user having the permission to remove, should remove this functionality|
|ac_customer_care_view|Only user having the permission to view, should view this functionality|
|ac_customer_care_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

## User Experience
### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
graph TD 
	CustomerCareMenu((Customer Care Menu))
	ListPage{Customer Care List Page}
	CreatePage((Create Page))
    RemovePage((Remove Page))
	ViewPage((ViewPage))
	DownloadFile>Save File On Disk]
	ErrorPage((ErrorPage))
	Stop((Stop))
	Start((Start))
	Start-->CustomerCareMenu
	subgraph Menu
    CustomerCareMenu
	end
	subgraph List
	CustomerCareMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	CustomerCareMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph Create
	ListPage--C-->CreatePage
	CreatePage--SB-->ListPage
	CreatePage--SB-->CreatePage
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
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 9 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px;
    linkStyle 12 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px; 
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;   
{{< /mermaid >}}



|Symbol|Action|
|:-----|:-----|
|C|Create|
|R|Remove|
|V|View|
|E|Export|
|B|Back|
|V-E|View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram
{{<mermaid align="center">}}
sequenceDiagram
    participant CustomerCareListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet, GET /app/CustomerCare/list ListPage
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S:  GET /app/CustomerCare/list ListPage
        cloud-->>-CustomerCareListPage: RES:List Page
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet, GET /app/CustomerCare/create/form CreateFormPage
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S : GET /app/CustomerCare/create/form CreateFormPage
        cloud-->>-CustomerCareListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: POST /app/CustomerCare/create Create
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S : POST /app/CustomerCare/create Create
        cloud-->>-CustomerCareListPage: RES: An CustomerCare Details Successfully Created
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: GET /app/CustomerCare/remove/form RemoveFormPage
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S : GET /app/CustomerCare/remove/form RemoveFormPage
        cloud-->>-CustomerCareListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: POST /app/CustomerCare/remove Remove
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S : POST /app/CustomerCare/remove Remove
        cloud-->>-CustomerCareListPage: RES: A CustomerCare Successfully Removed
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: GET /app/CustomerCare/view ViewPage
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: GET /app/CustomerCare/view ViewPage
        cloud-->>-CustomerCareListPage: RES: customerCare View
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: GET /app/CustomerCare/exportPdf ExportPdf
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: GET /app/CustomerCare/exportPdf ExportPdf
        cloud-->>-CustomerCareListPage: RES: customerCare Pdf
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: GET /app/CustomerCare/exportListPdf ExportListPdf
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S : GET /app/CustomerCare/exportListPdf ExportListPdf
        cloud-->>-CustomerCareListPage: RES: customerCare List Pdf
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: GET /app/CustomerCare/exportXlx ExportXlx
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: GET /app/CustomerCare/exportXlx ExportXlx
        cloud-->>-CustomerCareListPage: RES: customerCare Xlx
    end
    rect rgb(244,244,244)
        CustomerCareListPage->>+Net: Check Internet: GET /app/CustomerCare/exportListXlx ExportListXlx
        Net--x-CustomerCareListPage: F : Connection Error
        CustomerCareListPage->>+cloud: S : GET /app/CustomerCare/exportListXlx ExportListXlx
        cloud-->>-CustomerCareListPage: RES: customerCare List Xlx
    end
    
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|---|
|1.0| Create Form |ut_p_c_GSTS_WEB_CUSTOMERCARE_100|**Positive Test Cases:** 1.Open Paytm Payment Gateway Create Form|NA|1|0|1|testAuthorisedUserCreateCustomerCare|
|1.0| Create |ut_p_c_GSTS_WEB_CUSTOMERCARE_101 ut_n_c_GSTS_WEB_CUSTOMERCARE_102 ut_n_c_GSTS_WEB_CUSTOMERCARE_104 |**Positive Test Cases:** 1.Creating Customer Care with Authorized User **Negative Test Cases:** 1.Creating Customer Care with Invalid Inputs 2.Creating customer care without db connection|**name:** 1.Valid Characters 2.length>3 and length<64 3.null **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **category** **registerName:** 1.Valid Characters 2.length>3 and length<64 3.null **registerAadhaar:** 1.Valid characters 2.length=12 3.null **network**|4|2|6|testAuthorisedUserCreateCustomerCare, testAuthorisedUserCreateCustomerCareWithInvalidInputs, testAuthorisedUserCreateCustomerCareWithoutDBConnection|
|1.0| Remove Form |ut_p_r_GSTS_WEB_CUSTOMERCARE_200 ut_n_r_GSTS_WEB_CUSTOMERCARE_201 ut_n_r_GSTS_WEB_CUSTOMERCARE_203|**Positive Test Cases:** 1.Open Customer care Remove form with Authorized User **Negative Test Cases:** 1.Open Customer care Remove form with Invalid Id 2.Open Customer care Remove form without DB Connection|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserOpenCustomerCareRemoveForm, testAuthorisedUserOpenCustomerCareRemoveFormWithInvalidId, testAuthorisedUserOpenCustomerCareRemoveFormWithoutDBConnection|
|1.0| Remove|ut_p_r_GSTS_WEB_CUSTOMERCARE_209 ut_n_r_GSTS_WEB_CUSTOMERCARE_204 ut_n_r_GSTS_WEB_CUSTOMERCARE_205 ut_n_r_GSTS_WEB_CUSTOMERCARE_206 ut_n_r_GSTS_WEB_CUSTOMERCARE_208|**Positive Test Cases:** 1.Remove Customer care with Authorized User **Negative Test Cases:** 1.Remove Customer care with Invalid Comment 2.Remove Customer care with Invalid Comment and Id 3.Remove Customer care with Invalid Id 4.Remove Customer Care obj without DB Connection|**removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null|1|4|5|testAuthorisedUserRemoveCustomerCareWithInvalidInput, testAuthorisedUserRemoveCustomerCareWithInvalidCommentAndId, testAuthorisedUserRemoveCustomerCareWithInvalidId, testAuthorisedUserRemoveCustomerCareWithoutDBConnection, testAuthorisedUserRemoveCustomerCare|
|1.0| View |ut_p_v_GSTS_WEB_CUSTOMERCARE_300 ut_n_v_GSTS_WEB_CUSTOMERCARE_301 ut_n_v_GSTS_WEB_CUSTOMERCARE_303|**Positive Test Cases:** 1.View Customer care with Valid Id **Negative Test Cases:** 1.View Customer care with Invalid Id 2.View Customer care without DB Connection|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserViewCustomerCareWithValidId, testAuthorisedUserViewCustomerCareWithInvalidId, testAuthorisedUserViewCustomerCareWithoutDBConnection|
|1.0| Search |ut_p_s_GSTS_WEB_CUSTOMERCARE_400 ut_n_s_GSTS_WEB_CUSTOMERCARE_401 ut_n_s_GSTS_WEB_CUSTOMERCARE_403|**Positive Test Cases:** 1.Search Customer care with Authorized User **Negative Test Cases:** 1.Search Customer care with Invalid inputs 2.Search Customer care without DB Connection|**name:** 1.Valid Characters 2.length>3 and length<64 3.null **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **category** **registerAadhaar:** 1.Valid characters 2.length=12 3.null **network**|3|3|6|testAuthorisedUserSearchCustomerCare, testAuthorisedUserSearchCustomerCareWithInvalidInputs, testAuthorizedUserSearchCustomerCareWithoutDBConnection|
|1.0| List |ut_p_l_GSTS_WEB_CUSTOMERCARE_500 ut_n_l_GSTS_WEB_CUSTOMERCARE_501 ut_n_l_GSTS_WEB_CUSTOMERCARE_503|**Positive Test Cases:** 1.Check the object list with Valid data with Authorized User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User 2.Check the object list with Valid data without DB Connection|1.Valid Data 2.Invalid Data|1|2|3|testAuthorizedUserListCustomerCare, testAuthorizedUserListCustomerCareNegativeTestCase, testAuthorizedUserListCustomerCareWithoutDBConnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_CUSTOMERCARE_600 ut_n_ep_GSTS_WEB_CUSTOMERCARE_604 ut_n_ep_GSTS_WEB_CUSTOMERCARE_612 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_CUSTOMERCARE_601 ut_n_elp_GSTS_WEB_CUSTOMERCARE_605 ut_n_elp_GSTS_WEB_CUSTOMERCARE_613 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_CUSTOMERCARE_602 ut_n_ex_GSTS_WEB_CUSTOMERCARE_606 ut_n_ex_GSTS_WEB_CUSTOMERCARE_614 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_CUSTOMERCARE_603 ut_n_elx_GSTS_WEB_CUSTOMERCARE_607 ut_n_elx_GSTS_WEB_CUSTOMERCARE_615 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| Create |ut_n_c_GSTS_WEB_CUSTOMERCARE_103|UnAuthorized user does not have permission to create customer care|**name:** 1.Valid Characters 2.length>3 and length<64 3.null **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **category** **registerName:** 1.Valid Characters 2.length>3 and length<64 3.null **registerAadhaar:** 1.Valid characters 2.length=12 3.null **network**|0|1|1|testUnAuthorisedUserCreateCustomerCare|
|1.0| Remove Form |ut_n_r_GSTS_WEB_CUSTOMERCARE_202|Open Customer care Remove form with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenCustomerCareRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_CUSTOMERCARE_207|UnAuthorized user does not have permission to remove customer care|**removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null|0|1|1|testUnAuthorisedUserRemoveCustomerCare|
|1.0| View |ut_n_v_GSTS_WEB_CUSTOMERCARE_302|UnAuthorized user does not have permission to view customer care|1.Valid Id|0|1|1|testUnAuthorisedUserViewCustomerCare|
|1.0| Search |ut_n_s_GSTS_WEB_CUSTOMERCARE_402|UnAuthorized user does not have permission to search|NA|0|1|1|testUnAuthorizedUserSearchCustomerCare|
|1.0| List |ut_n_l_GSTS_WEB_CUSTOMERCARE_502|Check the object list with Valid data with UnAuthorised User|NA|0|1|1|testUnAuthorizedUserListCustomerCare|
|1.0| PDF |ut_n_ep_GSTS_WEB_CUSTOMERCARE_608 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_CUSTOMERCARE_609 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_CUSTOMERCARE_610 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_CUSTOMERCARE_611 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|

## Security compliance check
1. Only user having the permission **ROLE_CUSTOMER_CARE_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the customer care is provided in the User Manual.

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




 
