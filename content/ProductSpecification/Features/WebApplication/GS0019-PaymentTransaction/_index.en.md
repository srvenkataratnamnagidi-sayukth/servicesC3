---
title: GS0014 - Payment Transaction
tags : ["Composing"]
---

## Introduction
Payment Transaction is one of the features of our software product. The payment transaction feature stores data related to transactions while transactions takes place. Users should have permission to access this feature.

## Business Assumptions
Transactions data should be saved into database automatically.

## Requirements
### Functional Requirements
1. Users should view and export the payment transaction.
1. Any level of users can export and view the payment transaction.
1. we will save transaction's data into the database while transaction takes place.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access payment transactions.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Payment Transaction feature is required to store the data related to transactions.

### Design 
1. We can View and Export the payment Transaction.
1. Each payment transaction has payment id, order id, transaction date.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_payment_transaction_view|To view the payment transaction|
|uc_payment_transaction_search|To search the payment transaction|
|uc_payment_transaction_export|To export the payment transaction in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|invoice|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "invoice_id",  referencedColumnName = "id")|invoice_id VARCHAR(36) NOT NULL|YES|NO|NO||
|amt|YES|NA|NA|@Column(name = "amt", nullable = false)|amt float(9,2) NOT NULL|YES|YES|NO||
|rzpReceiptId|NO|NA|NA|@Column(name = "rzp_receipt_id", length = 64 ,nullable = true)|rzp_receipt_id VARCHAR(64) DEFAULT NULL|YES|NO|NO||
|currency|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "currency", length = 8, nullable = false)|currency varchar(8) NOT NULL|YES|NO|NO||
|rzpPartialPayment|NO|NA|NA|@Column(name = "rzp_partial_payment", nullable = true)|rzp_partial_payment boolean DEFAULT false|YES|NO|NO||
|notes|NO|NA|NA|@Column(name = "notes", length = 128 ,nullable = true)|notes VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|pgtype|NO|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "pgtype", length = 8 ,nullable = true)|pgtype varchar(8) DEFAULT NULL|YES|NO|NO||
|orderId|NO|NA|NA|@Column(name = "order_id", length = 128 ,nullable = true)|order_id VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|payment_id|NO|NA|NA|@Column(name = "payment_id", length = 128 ,nullable = true)|payment_id VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|rzpSignature|NO|NA|NA|@Column(name = "rzp_signature", length = 128 ,nullable = true)|rzp_signature VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|rzpResponseErrorCode|NO|NA|NA|@Column(name = "rzp_response_error_code", length = 64 ,nullable = true)|rzp_response_error_code VARCHAR(64) DEFAULT NULL|YES|NO|NO||
|rzpResponseErrorDescr|NO|NA|NA|@Column(name = "rzp_response_error_description", length = 256 ,nullable = true)|rzp_response_error_description VARCHAR(256) DEFAULT NULL|YES|NO|NO||
|rzpResponseErrorSource|NO|NA|NA|@Column(name = "rzp_response_error_source", length = 64 ,nullable = true)|rzp_response_error_source VARCHAR(64) DEFAULT NULL|YES|NO|NO||
|rzpResponseErrorStep|NO|NA|NA|@Column(name = "rzp_response_error_step", length = 64 ,nullable = true)|rzp_response_error_step VARCHAR(64) DEFAULT NULL|YES|NO|NO||
|rzpResponseErrorReason|YES|NA|NA|@Column(name = "rzp_response_error_reason", length = 64 ,nullable = true)|rzp_response_error_reason VARCHAR(64) DEFAULT NULL|YES|NO|NO||
|paymentStatus|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "payment_status", length = 8, nullable = true)|payment_status varchar(8) DEFAULT 'NOT_PAID'|YES|YES|YES||
|pgVendorType|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "pg_vendor_type", length = 8, nullable = true)|pg_vendor_type varchar(8) DEFAULT NULL|YES|YES|YES||
|paytmTransactionToken|NO|NA|NA|@Column(name = "paytm_txn_token", length = 128 ,nullable = true)|paytm_txn_token VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|paytmBankTxnId|NO|NA|NA|@Column(name = "paytm_bank_txnid", length = 128 ,nullable = true)|paytm_bank_txnid VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|paytmStatus|NO|NA|NA|@Column(name = "paytm_status", length = 128 ,nullable = true)|paytm_status VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|paytmRespCode|NO|NA|NA|@Column(name = "paytm_resp_code", length = 128 ,nullable = true)|paytm_resp_code VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|paytmRespMsg|NO|NA|NA|@Column(name = "paytm_resp_msg", length = 1024 ,nullable = true)|paytm_resp_msg VARCHAR(1024) DEFAULT NULL|YES|NO|NO||
|txnDate|NO|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "txn_date", nullable = true)|txn_date datetime DEFAULT NULL|YES|NO|NO||
|paytmGatewayName|NO|NA|NA|@Column(name = "paytm_gateway_name", length = 128 ,nullable = true)|paytm_gateway_name VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|paytmBankName|NO|NA|NA|@Column(name = "paytm_bank_name", length = 1024 ,nullable = true)|paytm_bank_name VARCHAR(1024) DEFAULT NULL|YES|NO|NO||
|paytmPaymentMode|NO|NA|NA|@Column(name = "paytm_payment_mode", length = 128 ,nullable = true)|paytm_payment_mode VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|paytmChecksumhash|NO|NA|NA|@Column(name = "paytm_checksumhash", length = 128 ,nullable = true)|paytm_checksumhash VARCHAR(128) DEFAULT NULL|YES|NO|NO||
|ownerMobileNumber|NO|NA|NA|@Column(name = "owner_mobile_number", length = 10, nullable = true)|owner_mobile_number varchar(10) DEFAULT NULL|YES|NO|YES||
|ownerMobileNumberMask|NO|NA|NA|@Column(name = "owner_mobile_number_mask", length = 10, nullable = true)|owner_mobile_number_mask varchar(10) DEFAULT NULL|YES|NO|NO||
|taxPayerMobileNumber|NO|NA|NA|@Column(name = "tax_payer_mobile_number", length = 10, nullable = true)|tax_payer_mobile_number varchar(10) DEFAULT NULL|YES|NO|YES||
|taxPayerMobileNumber|NO|NA|NA|@Column(name = "tax_payer_mobile_number", length = 10, nullable = true)|tax_payer_mobile_number varchar(10) DEFAULT NULL|YES|NO|NO||
|taxPayerMobileNumberMask|NO|NA|NA|@Column(name = "tax_payer_mobile_number_mask", length = 10, nullable = true)|tax_payer_mobile_number_mask varchar(10) DEFAULT NULL|YES|NO|NO||
|paymentStep|NO|NA|NA|@Column(name = "payment_step", length = 8 ,nullable = true)|payment_step varchar(8) DEFAULT NULL|YES|NO|NO||

#### Enum Constants

##### Currency Type

{{<mermaid align="left">}}
classDiagram
    class CurrencyType{
      INR
    }
{{< /mermaid >}}

##### Payment Gateway Type

{{<mermaid align="left">}}
classDiagram
    class PgType{
      CASH
      CHALLAN
      ONLINE
      NONE
    }
{{< /mermaid >}}

##### Payment Gateway Vendor

{{<mermaid align="left">}}
classDiagram
    class PgVendorType{
      RAZORPAY
      PAYTM
      SBI
      NONE
    }
{{< /mermaid >}}

##### Payment Status

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
|PAYMENT_TRANSACTION_VIEW|View|
|PAYMENT_TRANSACTION_VIEW|List|
|PAYMENT_TRANSACTION_VIEW|Search|
|PAYMENT_TRANSACTION_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_payment_transaction_view|Only user having the permission to view, should view this functionality|
|ac_payment_transaction_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

## User Experience
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
graph TD
    Start((start))
    End((end))
    Razorpay[Create Razorpay Merchant Account in Razorpay website]
    subgraph Create Payment Gateway Account
    PaymentGatewayAccount[Payment Gateway Menu]
    ListPage[Payment Gateway Account Listing Page]
    PaymentGatewayAccountCreateForm[Payment Gateway Account Create Form Page]
    DataValidationCheck{Data Validation}
	ShowMessageDataValidation>Show Message: Please Enter Valid Data]
	CreatePaymentGatewayAccount[Create Payment Gateway Account]
    end
    subgraph Payment Process
    Administration[Administration Menu]
    Invoice[Invoice List Page]
    InvoicePay[Payment View Page]
    Gateway[Select Payment Gateway Page]
    Order[Create Order for Payment]
    CheckoutConfig[Assign Values to Checkout configuration]
    RazorpayCheckout{Checkout Form}
    VerifySignature{Verify Signature}
    FailureResponse[Store Reponse in DB]
    SuccessReponse[Store Response in DB]
    InvalidSignatureResponse[Store Response in DB]
    Retry[Retry]
    end
    Start--Step-1-->Razorpay
    Start--Step-2-->PaymentGatewayAccount
    Start--Step-3-->Administration
    PaymentGatewayAccount--Click Payment Gateway Account-->ListPage
    ListPage--Create-->PaymentGatewayAccountCreateForm
    PaymentGatewayAccountCreateForm--input form data-->DataValidationCheck
    DataValidationCheck--Not Valid-->ShowMessageDataValidation
    DataValidationCheck--Valid-->CreatePaymentGatewayAccount
    Administration--Click Invoice-->Invoice
    Invoice--Pay-->InvoicePay
    InvoicePay--Next-->Gateway
    Gateway--Click on Gateway-->Order
    Order--Order Response-->CheckoutConfig
    CheckoutConfig--Invoke Checkout Form-->RazorpayCheckout
    RazorpayCheckout--Reponse:Payment Success-->VerifySignature
    RazorpayCheckout--Reponse:Payment Failure-->FailureResponse
    VerifySignature--Valid-->SuccessReponse
    VerifySignature--Not Valid-->InvalidSignatureResponse
    SuccessReponse--Success Message-->Invoice
    InvalidSignatureResponse--Failure Message-->Invoice
    FailureResponse--Retry-->Retry
    Razorpay-->End
	CreatePaymentGatewayAccount-->End
	
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
graph TD 
	PaymentTransactionMenu((Payment Transaction Menu))
	ListPage{Payment Transaction List Page}
	ViewPage((ViewPage))
	DownloadFile>Save File On Disk]
	ErrorPage((ErrorPage))
	Stop((Stop))
	Start((Start))
	Start-->PaymentTransactionMenu
	subgraph Menu
    PaymentTransactionMenu
	end
	subgraph List
	PaymentTransactionMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	PaymentTransactionMenu-->ErrorPage
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
1. Only a user with the ROLE_PAYMENT_TRANSACTION_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant PaymentTransactionListPage as Browser
    participant Net as Browser Net Tools
   	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PaymentTransactionListPage->>+Net: Check Internet, GET /app/ctx/PaymentTransaction/list ListPage
        Net--x-PaymentTransactionListPage: F : Connection Error
        PaymentTransactionListPage->>+cloud: S:  GET /app/ctx/PaymentTransaction/list ListPage
        cloud-->>-PaymentTransactionListPage: RES:List Page
    end
    rect rgb(244,244,244)
        PaymentTransactionListPage->>+Net: Check Internet: GET /app/PaymentTransaction/view ViewPage
        Net--x-PaymentTransactionListPage: F : Connection Error
        PaymentTransactionListPage->>+cloud: GET /app/PaymentTransaction/view ViewPage
        cloud-->>-PaymentTransactionListPage: RES: Payment Transaction View
    end
    rect rgb(244,244,244)
        PaymentTransactionListPage->>+Net: Check Internet: GET /app/PaymentTransaction/exportPdf ExportPdf
        Net--x-PaymentTransactionListPage: F : Connection Error
        PaymentTransactionListPage->>+cloud: GET /app/PaymentTransaction/exportPdf ExportPdf
        cloud-->>-PaymentTransactionListPage: RES: Payment Transaction Pdf
    end
    rect rgb(244,244,244)
        PaymentTransactionListPage->>+Net: Check Internet: GET /app/PaymentTransaction/exportListPdf ExportListPdf
        Net--x-PaymentTransactionListPage: F : Connection Error
        PaymentTransactionListPage->>+cloud: S : GET /app/PaymentTransaction/exportListPdf ExportListPdf
        cloud-->>-PaymentTransactionListPage: RES: Payment Transaction List Pdf
    end
    rect rgb(244,244,244)
        PaymentTransactionListPage->>+Net: Check Internet: GET /app/PaymentTransaction/exportXlx ExportXlx
        Net--x-PaymentTransactionListPage: F : Connection Error
        PaymentTransactionListPage->>+cloud: GET /app/PaymentTransaction/exportXlx ExportXlx
        cloud-->>-PaymentTransactionListPage: RES: Payment Transaction Xlx
    end
    rect rgb(244,244,244)
        PaymentTransactionListPage->>+Net: Check Internet: GET /app/PaymentTransaction/exportListXlx ExportListXlx
        Net--x-PaymentTransactionListPage: F : Connection Error
        PaymentTransactionListPage->>+cloud: S : GET /app/PaymentTransaction/exportListXlx ExportListXlx
        cloud-->>-PaymentTransactionListPage: RES: Payment Transaction List Xlx
    end
          
{{< /mermaid >}}


## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
||||
||||

## Security compliance check
1. Only user having the user role with permission **ROLE_PAYMENT_TRANSACTION_VIEW** should view this functionality 
1. Only user having the user role with permission **ROLE_PAYMENT_TRANSACTION_VIEW** should export this functionality 


## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the PAYMENT TRANSACTION in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
