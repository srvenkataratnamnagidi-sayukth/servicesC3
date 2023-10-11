---
title: Invoice
tags : ["Composing"]
---

## Introduction
Invoice is one of the features of this software product. Using this feature we can display invoice generated for the tax of different properties (House/Kolagaram/Advertisement/Trade/Vacantland) in every financial year. Users will have access to Invoice if they have permission, Otherwise will not access.

## Business Assumptions
1. What type of users can access Invoice should be planned at design phase.
1. Payment should be completed for each invoice.

## Requirements
### Functional Requirements
1. Invoice feature is accessible at panchayat level only.
1. Property should be required to generate the invoice for the property.
1. Only one invoice should be created for one property tax.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access Invoice.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Invoice function is used to list out all the invoices for every Tax Invoice Generated in financial year at panchayat.

### Design 
1. Each invoice has amount, arrears, surcharge, discount, total amount, due date, property type, invoice type and payment status.
1. This feature is used to store and list out all the invoice.
1. We can view and export the Invoice.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	
	
#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_invoice_list|To view all the invoice. This listing page should bind to a permission|
|uc_invoice_view|To view the invoice. This view page should bind to a permission|
|uc_invoice_search|To search the invoice. This search page should bind to a permission|
|uc_invoice_export|To export the invoice rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|uuid|YES|NA|NA|@Column(name = "uuid", length = 64, nullable = false, unique = true)|uuid varchar(64) NOT NULL|YES|NO|NO||
|status|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "status", length = 8, nullable = false)|status varchar(8) NOT NULL|YES|NO|NO||
|amt|YES|NA|NA|@Column(name = "amt", nullable = false)|amt float(9,2) NOT NULL|YES|YES|NO||
|arrears|YES|NA|NA|@Column(name = "arrears", nullable = false)|arrears float(9,2) NOT NULL|YES|YES|NO||
|sc|YES|NA|NA|@Column(name = "sc", nullable = false)|sc float(9,2) NOT NULL|YES|YES|NO||
|discount|YES|NA|NA|@Column(name = "discount", nullable = false)|discount float(9,2) NOT NULL|YES|YES|NO||
|total|YES|NA|NA|@Column(name = "total", nullable = false)|total float(9,2) NOT NULL|YES|YES|NO||
|due|NO|NA|NA|DateTimeFormat(pattern = "dd-MM-yyyy")@Temporal(TemporalType.TIMESTAMP)@Column(name = "due", nullable = true)|due datetime NOT NULL|YES|NO|NO||
|property|NO|NA|NA|@ManyToOne(fetch = FetchType.LAZY)@JoinColumn(name = "property_id", nullable = true)|property_id VARCHAR(36) DEFAULT NULL|YES|NO|NO||
|propertyType|NO|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "property_type", length = 16, nullable = true)|property_type varchar(16) DEFAULT NULL|YES|YES|YES||
|email|NO|NA|NA|@Column(name = "email", length = 64, nullable = true)|email varchar(64) DEFAULT NULL|YES|NO|NO||
|mobile|NO|NA|NA|@Column(name = "mobile", length = 15, nullable = true)|mobile varchar(15) DEFAULT NULL|YES|NO|NO||
|txnId|NO|NA|NA|@Column(name = "txnid", nullable = true)|txnid varchar(64) DEFAULT NULL|YES|NO|NO||
|invoiceType|YES|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "invoice_type", length = 32, nullable = false)|invoice_type varchar(32) NOT NULL|YES|YES|YES||
|year|YES|NA|NA|@Column(name = "year", length = 16, nullable = false)|year bigint(20) NOT NULL|YES|YES|YES||
|pgtype|YES|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "pgtype", length = 8, nullable = false)|pgtype varchar(8) NOT NULL|YES|NO|NO||
|pgVendorType|NO|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "pg_vendor_type", length = 8, nullable = true)|pg_vendor_type varchar(8) DEFAULT NULL|YES|YES|NO||
|paymentStatus|NO|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "payment_status", length = 8, nullable = true)|payment_status varchar(8) DEFAULT 'NOT_PAID'|YES|YES|NO||
|txnDate|NO|NA|NA|DateTimeFormat(pattern = "dd-MM-yyyy")@Temporal(TemporalType.TIMESTAMP)@Column(name = "txn_date", nullable = true)|txn_date datetime NOT NULL|YES|NO|NO||

#### ENUM CONSTANTS
##### InvoiceStatusType

{{<mermaid align="left">}}
classDiagram
    class InvoiceStatusType{
      EXPIRED
      NEW
      PAID
      WIP
      FAILED
    }
{{< /mermaid >}}

##### PropertyCatType

{{<mermaid align="left">}}
classDiagram
    class PropertyCatType{
      HOUSE
      ADVERTISEMENT
      KOLAGARAM
      TRADE_LICENSE
      AUCTION
      VACANT_LAND
      OTHER
    }
{{< /mermaid >}}

##### PgType

{{<mermaid align="left">}}
classDiagram
    class PgType{
      CASH
      CHALLAN
      ONLINE
      NONE
    }
{{< /mermaid >}}

##### PgVendorType

{{<mermaid align="left">}}
classDiagram
    class PgVendorType{
     RAZORPAY
     PAYTM
     SBI
     NONE
    }
{{< /mermaid >}}

##### PaymentStatus

{{<mermaid align="left">}}
classDiagram
    class PaymentStatus{
     PAID
     NOT_PAID
    }
{{< /mermaid >}}

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|INVOICE_VIEW|View|
|INVOICE_VIEW|Export|
|INVOICE_VIEW|List|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_INVOICE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_INVOICE_VIEW|Only user having the user role with this permission should export the invoice in 2 formats Excel, PDF|

## User Experience
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
graph TD 
	InvoiceMenu((Invoice Menu))
	ListPage{Invoice List Page}
	ViewPage((ViewPage))
	DownloadFile>Save File On Disk]
	ErrorPage((ErrorPage))
	Stop((Stop))
	Start((Start))
	Start-->InvoiceMenu
	subgraph Menu
    InvoiceMenu
	end
	subgraph List
	InvoiceMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	InvoiceMenu-->ErrorPage
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
|S|Submit|
|B|Back|
|SB|Submit or Back|
|V-E|View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the ROLE_INVOICE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant InvoiceListPage as Browser
    participant Net as Browser Net Tools
   	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        InvoiceListPage->>+Net: Check Internet, GET /app/ctx/Invoice/list ListPage
        Net--x-InvoiceListPage: F : Connection Error
        InvoiceListPage->>+cloud: S:  GET /app/ctx/Invoice/list ListPage
        cloud-->>-InvoiceListPage: RES:List Page
    end
    rect rgb(244,244,244)
        InvoiceListPage->>+Net: Check Internet: GET /app/Invoice/view ViewPage
        Net--x-InvoiceListPage: F : Connection Error
        InvoiceListPage->>+cloud: GET /app/Invoice/view ViewPage
        cloud-->>-InvoiceListPage: RES: Invoice View
    end
    rect rgb(244,244,244)
        InvoiceListPage->>+Net: Check Internet: GET /app/Invoice/exportPdf ExportPdf
        Net--x-InvoiceListPage: F : Connection Error
        InvoiceListPage->>+cloud: GET /app/Invoice/exportPdf ExportPdf
        cloud-->>-InvoiceListPage: RES: Invoice Pdf
    end
    rect rgb(244,244,244)
        InvoiceListPage->>+Net: Check Internet: GET /app/Invoice/exportListPdf ExportListPdf
        Net--x-InvoiceListPage: F : Connection Error
        InvoiceListPage->>+cloud: S : GET /app/Invoice/exportListPdf ExportListPdf
        cloud-->>-InvoiceListPage: RES: Invoice List Pdf
    end
    rect rgb(244,244,244)
        InvoiceListPage->>+Net: Check Internet: GET /app/Invoice/exportXlx ExportXlx
        Net--x-InvoiceListPage: F : Connection Error
        InvoiceListPage->>+cloud: GET /app/Invoice/exportXlx ExportXlx
        cloud-->>-InvoiceListPage: RES: Invoice Xlx
    end
    rect rgb(244,244,244)
        InvoiceListPage->>+Net: Check Internet: GET /app/Invoice/exportListXlx ExportListXlx
        Net--x-InvoiceListPage: F : Connection Error
        InvoiceListPage->>+cloud: S : GET /app/Invoice/exportListXlx ExportListXlx
        cloud-->>-InvoiceListPage: RES: Invoice List Xlx
    end
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|
|||||||||

#### UnAuthorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|
|||||||||

## Security compliance check
1. Only user having the permission **ROLE_INVOICE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_INVOICE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Invoice in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0002|[GS-0002](https://shadkona.atlassian.net/browse/GS-0002)|Closed|


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




 
