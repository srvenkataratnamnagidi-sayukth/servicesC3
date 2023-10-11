---
title: GS0014 - Payment Gateway
tags : ["Composing"]
---

## Introduction
Payment gateway is one of the features of our software product. The payment gateway feature works as the middleman between the citizens and the panchayat officials, ensuring the transaction is carried out securely and promptly. Users should have permission to access this feature.

## Business Assumptions
Creating, updating and removing the payment gateway can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
Only panchayat level users should create, update, remove or view the payment gateway.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access assets.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Payment gateway feature is required to capture and transfer payment data from the citizen to the acquirer.

### Design 
1. We can Create, Update, View, and remove the payment gateway.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_payment_gateway_create|To create the payment gateway|
|uc_payment_gateway_update|To update the payment gateway|
|uc_payment_gateway_remove|To remove the payment gateway|
|uc_payment_gateway_view|To view the payment gateway|
|uc_payment_gateway_search|To search the payment gateway|
|uc_payment_gateway_export|To export the payment gateway in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Name|YES|NA|Allowed a-z, A-Z, 0-9, space,_ ,- and length 3 to 64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) not null|YES|NO|YES|YES|YES|YES||
|Description|YES|NA|Allowed a-z, A-Z, 0-9, space, _, - |@Column(name = "descr", length = 1024, nullable = false)|descr varchar(1024) not null|YES|NO|YES|YES|YES|NO||
|Mobile Number|YES|NA|Allowed only 0-9 |@Column(name = "mobile", length = 13, nullable = true)|mobile varchar(13) default null|YES|NO|YES|YES|YES|NO||
|Email|YES|NA|Allowed a-z , A-Z , 0-9 , @ , . , _ and length 3 to 64|@Column(name = "email", length = 64, nullable = true)|email varchar(13) default null|YES|NO|YES|YES|YES|NO||
|Payment Gateway Type|YES|NA|Drop Down List|@Enumerated(EnumType.STRING) @Column(name = "pgtype", length = 12, nullable = false)|pgtype varchar(12) not null|YES|NO|YES|YES|YES|YES||
|Paytm Merchant Id|YES|NA|Allowed a-z, A-Z, 0-9, space, _, - |@Column(name = "pytm_mid", length = 36, nullable = true)|pytm_mid varchar(36) default null|YES|YES|YES|YES|NO|NO||
|Paytm Website|YES|NA|Allowed a-z , A-Z , 0-9 , space , _ , - |@Column(name = "pytm_website", length = 12, nullable = true)|pytm_website varchar(12) default null|YES|YES|YES|YES|NO|NO||
|Paytm Url Format|YES|NA|Allowed a-z , A-Z , 0-9 , space , _ , -|@Column(name = "pytm_url", length = 64, nullable = true)|pytm_url varchar(64) default null|YES|YES|YES|YES|NO|NO||
|Paytm Call Back Url |YES|NA|Allowed a-z , A-Z , 0-9 , space , _ , -|@Column(name = "pytm_cburl", length = 64, nullable = true)|pytm_cburl varchar(64) default null|YES|YES|YES|YES|NO|NO||
|Paytm Charge |YES|NA|Allowed 0-9 and .|@Column(name = "pytm_sc" , nullable = true)|pytm_sc  float(9,2) default null|YES|YES|YES|YES|NO|NO||
|Updated Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|Removed Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### Enum Constants

##### Payment Gateway Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      PAYTM
      SBI
      CASH
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|PAYMENT_CREATE|Create|
|PAYMENT_UPDATE|Update|
|PAYMENT_REMOVE|Remove|
|PAYMENT_VIEW|View|
|PAYMENT_VIEW|List|
|PAYMENT_VIEW|Export|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_payment_create|Only user having the permission to create, should create this functionality|
|ac_payment_update|Only user having the permission to update, should update this functionality|
|ac_payment_remove|Only user having the permission to remove, should remove this functionality|
|ac_payment_view|Only user having the permission to view, should view this functionality|
|ac_payment_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

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
	PaymentGatewayMenu((Payment Gateway Menu))
	ListPage{Payment Gateway List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->PaymentGatewayMenu
    subgraph Menu
    PaymentGatewayMenu
	end
	subgraph List
	PaymentGatewayMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	PaymentGatewayMenu-->ErrorPage
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
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-V-E|Create or Update or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant PaymentGatewayListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet, GET /app/ctx/Payment/list ListPage
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S:  GET /app/ctx/Payment/list ListPage
        cloud-->>-PaymentGatewayListPage: RES:List Page
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet, GET /app/PaymentGatewayAccount/paytm/create/form CreateFormPage
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : GET /app/PaymentGatewayAccount/paytm/create/form CreateFormPage
        cloud-->>-PaymentGatewayListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/paytm/create Create
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : POST /app/PaymentGatewayAccount/paytm/create Create
        cloud-->>-PaymentGatewayListPage: RES: An Payment Gateway Account Successfully Created
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/update/form UpdateFormPage
        Net--x-PaymentGatewayListPage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Account Cache Object Found
        PaymentGatewayListPage->>+Cache: S : GET /app/PaymentGatewayAccount/update/form UpdateFormPage
        Cache-->>-PaymentGatewayListPage: RES: Update Form Loaded
        else
        Note right of Net: Payment Gateway Account Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/update/form UpdateFormPage
        cloud-->>-PaymentGatewayListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/update update
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : POST /app/PaymentGatewayAccount/update Update
        cloud-->>-PaymentGatewayListPage: RES: An Payment Gateway Account Successfully Updated
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/remove/form RemoveFormPage
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : GET /app/PaymentGatewayAccount/remove/form RemoveFormPage
        cloud-->>-PaymentGatewayListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/remove Remove
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : POST /app/PaymentGatewayAccount/remove Remove
        cloud-->>-PaymentGatewayListPage: RES: A Payment Gateway Account Successfully Removed
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/view ViewPage
        Net--x-PaymentGatewayListPage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Account Cache Object Found
        PaymentGatewayListPage->>+Cache: S : GET /app/PaymentGatewayAccount/view ViewPage
        Cache-->>-PaymentGatewayListPage: RES: paymentGateway View
        else
        Note right of Net: Payment Gateway Account Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/view ViewPage
        cloud-->>-PaymentGatewayListPage: RES: paymentGateway View
        end
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportPdf ExportPdf
        Net--x-PaymentGatewayListPage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Account Cache Object Found
        PaymentGatewayListPage->>+Cache: S : GET /app/PaymentGatewayAccount/exportPdf ExportPdf
        Cache-->>-PaymentGatewayListPage: RES: paymentGateway Pdf
        else
        Note right of Net: Payment Gateway Account Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/exportPdf ExportPdf
        cloud-->>-PaymentGatewayListPage: RES: paymentGateway Pdf
        end
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportListPdf ExportListPdf
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : GET /app/PaymentGatewayAccount/exportListPdf ExportListPdf
        cloud-->>-PaymentGatewayListPage: RES: paymentGateway List Pdf
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportXlx ExportXlx
        Net--x-PaymentGatewayListPage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Account Cache Object Found
        PaymentGatewayListPage->>+Cache: S : GET /app/PaymentGatewayAccount/exportXlx ExportXlx
        Cache-->>-PaymentGatewayListPage: RES: paymentGateway Xlx
        else
        Note right of Net: Payment Gateway Account Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/exportXlx ExportXlx
        cloud-->>-PaymentGatewayListPage: RES: paymentGateway Xlx
        end
    end
    rect rgb(244,244,244)
        PaymentGatewayListPage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportListXlx ExportListXlx
        Net--x-PaymentGatewayListPage: F : Connection Error
        PaymentGatewayListPage->>+cloud: S : GET /app/PaymentGatewayAccount/exportListXlx ExportListXlx
        cloud-->>-PaymentGatewayListPage: RES: paymentGateway List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
||||
||||

## Security compliance check
1. Only user having the user role with permission **ROLE_PAYMENT_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_PAYMENT_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_PAYMENT_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_PAYMENT_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the PAYMENT GATEWAY in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
