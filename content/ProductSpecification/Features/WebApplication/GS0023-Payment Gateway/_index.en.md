---
title: GS0023 - Payment Gateway Account
tags : ["Composing"]
---

## Introduction
Payment Gateway Account is one of the feature of this software product. The primary role of the payment gateway account is to store the information of the merchant account. A payment gateway is a technology used by merchants to process online payments from customers. A payment gateway facilitates a payment transaction by the transfer of information between a payment portal and the front end processor. Payment gateway account is a service that helps merchants initiate payment by providing the required information.

## Business Assumptions
1. Payment Gateway should be maintained (i.e. creation and updation) by the organization .
2. Payment Gateway is secured and reliable.

## Requirements
### Functional Requirements
1. A payment gateway is the feature that transfers merchant account information from server to a payment gateway.
2. Payment Gateway feature provides input to create an order.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access payment gateway.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Payment Gateway is required to provide information to each transaction initiated by the user.

### Design 
1. Each Payment Gateway has merchant user information and organization information. 
1. We can create, update, remove, view and export the payment gateway.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_payment_gateway_create|To create the payment gateway. This create page should bind to a permission|
|uc_payment_gateway_update|To update the payment gateway. This update page should bind to a permission|
|uc_payment_gateway_remove|To remove the payment gateway. This remove page should bind to a permission|
|uc_payment_gateway_list|To view all the payment gateways. This listing page should bind to a permission|
|uc_payment_gateway_view|To view the payment gateway. This view page should bind to a permission|
|uc_payment_gateway_search|To search the payment gateway. This search page should bind to a permission|
|uc_payment_gateway_export|To export the payment gateway in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|----|------|-------|
|name|YES|NA|a-zA-Z0-9. space _-, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|YES|YES|YES|YES|NO||
|mobile|YES|NA|0-9 len=10|@Column(name = "mobile", length = 13, nullable = false)|mobile varchar(13) NOT NULL|YES|YES|YES|YES|YES|NO||
|pgSupportContact|YES|NA|0-9 minlen=10 , maxlen=13|@Column(name = "pg_supportcontact", length = 13, nullable = false)|pg_supportcontact varchar(13) NOT NULL|YES|YES|YES|YES|NO|NO||
|email|YES|NA|NA|@Column(name = "email", length = 64, nullable = false)|email varchar(64) NOT NULL|YES|YES|YES|YES|YES|NO||
|pgtype|YES|NA|Enum Values|@Enumerated(EnumType.STRING) @Column(name = "pgtype", length = 12, nullable = false)|pgtype varchar(12) NOT NULL|YES|YES|YNO|NO|NO|YES||
|pgVendorType|YES|NA|Enum Values|@Enumerated(EnumType.STRING)@Column(name = "pg_vendor_type", length = 8, nullable = false)|pg_vendor_type varchar(8) NOT NULL|YES|YES|YES|YES|YES|NO||
|pgWebsite|YES|NA|NA|@Column(name = "pg_website", length = 128, nullable = false)|pg_website varchar(128) NOT NULL|YES|YES|YES|YES|NO|NO||
|pgLogo|YES|NA|NA|@Column(name = "pg_logo", length = 255, nullable = false)|pg_logo varchar(255) NOT NULL|YES|YES|YES|NO|NO|NO||
|pgMid|YES|NA|NA|@Column(name = "pg_mid", length = 36, nullable = false)|pg_mid varchar(36) NOT NULL|YES|YES|YES|YES|NO|NO||
|pgMkey|YES|NA|NA|@Column(name = "pg_mkey", length = 36, nullable = false)|pg_mkey varchar(36) NOT NULL|YES|YES|YES|YES|NO|NO||
|pgCurrency|YES|NA|Enum Values|@Enumerated(EnumType.STRING)@Column(name = "pg_currency", length = 36, nullable = false)|pg_currency varchar(36) NOT NULL|YES|YES|YES|YES|NO|NO||
|pgCallbackurl|NO|NA|NA|@Column(name = "pg_cburl", length = 128, nullable = true)|pg_cburl varchar(128) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|pgPaymentMethods|YES|NA|NA|@Column(name = "pg_payment_methods", length = 128, nullable = false)|pg_payment_methods varchar(128) NOT NULL|YES|YES|YES|YES|NO|NO||
|merchantLogo|YES|NA|NA|@Column(name = "merchant_logo", length = 255, nullable = false)|merchant_logo varchar(255) NOT NULL|YES|YES|YES|NO|NO|NO||
|merchantName|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=3, maxlen=64|@Column(name = "merchant_name", length = 64, nullable = false)|merchant_name varchar(64) NOT NULL|YES|YES|YES|YES|NO|NO||
|merchantDescr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "merchant_descr", length = 256, nullable = false)|merchant_descr varchar(256) NOT NULL|YES|YES|YES|YES|NO|NO||
|pytmRequestType|YES|NA|Enum|@Enumerated(EnumType.STRING)@Column(name = "pytm_request_type", length = 36, nullable = true)|pytm_request_type varchar(36) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|pytmWebsiteName|YES|NA|Enum|@Enumerated(EnumType.STRING)@Column(name = "pytm_website", length = 36, nullable = true)|pytm_website varchar(36) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|pytmRoot|YES|NA|NA|@Column(name = "pytm_root", length = 36, nullable = true)|pytm_root varchar(36) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|pytmFlow|YES|NA|Enum|@Enumerated(EnumType.STRING)@Column(name = "pytm_flow", length = 36, nullable = true)|pytm_flow varchar(36) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|pytmTokenType|YES|NA|Enum|@Enumerated(EnumType.STRING)@Column(name = "pytm_token_type", length = 36, nullable = true)|pytm_token_type varchar(36) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|pytmUrl|YES|NA|NA|@Column(name = "pytm_url", length = 255, nullable = true)|pytm_url varchar(255) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|rzpPartialPayment|YES|NA|Boolean|@Column(name = "rzp_partial_payment", nullable = true)|rzp_partial_payment boolean DEFAULT false|YES|YES|YES|YES|NO|NO||
|serviceCharge|YES|NA|0-9.|@Column(name = "service_charge", nullable = false)|service_charge float(9,2) NOT NULL|YES|YES|YES|YES|NO|NO||
|stateGst|YES|NA|0-9.|@Column(name = "state_gst", nullable = false)|state_gst float(9,2) NOT NULL|YES|YES|YES|YES|NO|NO||
|centralGst|YES|NA|0-9.|@Column(name = "central_gst", nullable = false)|central_gst float(9,2) NOT NULL|YES|YES|YES|YES|NO|NO||



#### ENUM CONSTANTS
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

##### Currency Type

{{<mermaid align="left">}}
classDiagram
    class CurrencyType{
      INR
    }
{{< /mermaid >}}

##### Paytm Website Type

{{<mermaid align="left">}}
classDiagram
    class PaytmWebsiteType{
      WEBSTAGING
      DEFAULT
    }
{{< /mermaid >}}

##### Paytm Flow Type

{{<mermaid align="left">}}
classDiagram
    class PaytmFlowType{
      DEFAULT 
    }
{{< /mermaid >}} 
   
##### Paytm Token Type

{{<mermaid align="left">}}
classDiagram
    class PaytmTokenType{
      TXN_TOKEN
    }
{{< /mermaid >}} 

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|PAYMENT_CREATE|Create|
|PAYMENT_UPDATE|Update|
|PAYMENT_REMOVE|Remove|
|PAYMENT_VIEW|Export|
|PAYMENT_VIEW|List|
|PAYMENT_VIEW|View|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_PAYMENT_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_PAYMENT_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_PAYMENT_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_PAYMENT_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_PAYMENT_VIEW|Only user having the user role with this permission should list this functionality|
|AC_ROLE_PAYMENT_VIEW|Only user having the user role with this permission should export the payment gateway in 2 formats Excel, PDF|

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
    CreateBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
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
	subgraph   
    PaymentGatewayMenu-->ListPage
    ListPage--C-U-R-V-E-->ListPage
    end
    subgraph  
    PaymentGatewayMenu--F-->ErrorPage
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
    subgraph Remove
    ListPage--R-->RemovePage
    RemovePage--SB-->ListPage
    RemovePage--SB-->RemovePage
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
|:-----|:-----|
|C|Create|
|U|Update|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|C-U-R-V-E|Create or Update or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the ROLE_PAYMENT_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant PaymentListpage as Browser
    participant Net as Browser Net Tools
   	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet, GET /app/ctx/Payment/list ListPage
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S:  GET /app/ctx/Payment/list ListPage
        cloud-->>-PaymentListpage: RES:List Page
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet, GET /app/PaymentGatewayAccount/paytm/create/form PaytmCreateFormPage
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : GET /app/PaymentGatewayAccount/paytm/create/form PaytmCreateFormPage
        cloud-->>-PaymentListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/paytm/create Create
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : POST /app/PaymentGatewayAccount/paytm/create Create
        cloud-->>-PaymentListpage: RES: Payment Gateway Successfully Created
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet, GET /app/PaymentGatewayAccount/razorpay/create/form RazorpayCreateFormPage
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : GET /app/PaymentGatewayAccount/razorpay/create/form RazorpayCreateFormPage
        cloud-->>-PaymentListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/razorpay/create Create
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : POST /app/PaymentGatewayAccount/razorpay/create Create
        cloud-->>-PaymentListpage: RES: Payment Gateway Successfully Created
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet, GET /app/PaymentGatewayAccount/update/form UpdateFormPage
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : GET /app/PaymentGatewayAccount/update/form UpdateFormPage
        cloud-->>-PaymentListpage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/update Update
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : POST /app/PaymentGatewayAccount/update update
        cloud-->>-PaymentListpage: RES: Payment Gateway Successfully Updated
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/remove/form RemoveFormPage
        Net--x-PaymentListpage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Cache Object Found
        PaymentListpage->>+Cache: S : GET /app/PaymentGatewayAccount/remove/form RemoveFormPage
        Cache-->>-PaymentListpage: RES: Remove Form Loaded
        else
        Note right of Net: Payment Gateway Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/remove/form RemoveFormPage
        cloud-->>-PaymentListpage: RES: Remove Form Loaded
        end
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: POST /app/PaymentGatewayAccount/remove Remove
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : POST /app/PaymentGatewayAccount/remove Remove
        cloud-->>-PaymentListpage: RES: Payment Gateway Successfully Removed
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/view ViewPage
        Net--x-PaymentListpage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Cache Object Found
        PaymentListpage->>+Cache: S : GET /app/PaymentGatewayAccount/view ViewPage
        Cache-->>-PaymentListpage: RES: Payment Gateway View
        else
        Note right of Net: Payment Gateway Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/view ViewPage
        cloud-->>-PaymentListpage: RES: Payment Gateway View
        end
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportPdf ExportPdf
        Net--x-PaymentListpage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Cache Object Found
        PaymentListpage->>+Cache: S : GET /app/PaymentGatewayAccount/exportPdf ExportPdf
        Cache-->>-PaymentListpage: RES: Payment Gateway Pdf
        else
        Note right of Net: Payment Gateway Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/exportPdf ExportPdf
        cloud-->>-PaymentListpage: RES: Payment Gateway Pdf
        end
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportListPdf ExportListPdf
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : GET /app/PaymentGatewayAccount/exportListPdf ExportListPdf
        cloud-->>-PaymentListpage: RES: Payment Gateway List Pdf
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportXlx ExportXlx
        Net--x-PaymentListpage: F : Connection Error
        alt
        Note right of Net: Payment Gateway Cache Object Found
        PaymentListpage->>+Cache: S : GET /app/PaymentGatewayAccount/exportXlx ExportXlx
        Cache-->>-PaymentListpage: RES: Payment Gateway Xlx
        else
        Note right of Net: Payment Gateway Cache Object Not Found
        Cache->>+cloud: GET /app/PaymentGatewayAccount/exportXlx ExportXlx
        cloud-->>-PaymentListpage: RES: Payment Gateway Xlx
        end
    end
    rect rgb(244,244,244)
        PaymentListpage->>+Net: Check Internet: GET /app/PaymentGatewayAccount/exportListXlx ExportListXlx
        Net--x-PaymentListpage: F : Connection Error
        PaymentListpage->>+cloud: S : GET /app/PaymentGatewayAccount/exportListXlx ExportListXlx
        cloud-->>-PaymentListpage: RES: Payment Gateway List Xlx
    end
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-----------------|-----|
|1.0| Create Form |ut_p_c_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_120 ut_p_c_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_130 |**Positive Test Cases:** 1.Open Paytm Payment Gateway Create Form  2.Open Razorpay Payment Gateway Create Form|-|2||2|testPosOpenPaytmPaymentGatewayCreateFormWithAuthorisedUser,  testPosOpenRazorpayPaymentGatewayCreateFormWithAuthorisedUser|
|1.0| Create | ut_p_c_GSTS_WEB_PAYMENT_GATEWAY_150 ut_p_c_GSTS_WEB_PAYMENT_GATEWAY_170 ut_n_c_GSTS_WEB_PAYMENT_GATEWAY_160  ut_n_c_GSTS_WEB_PAYMENT_GATEWAY_180  ut_n_c_GSTS_WEB_PAYMENT_GATEWAY_140  ut_n_c_GSTS_WEB_PAYMENT_GATEWAY_145|**Positive Test Cases:** 1.Create Razorpay Payment Gateway with valid inputs   2.Create Paytm Payment Gateway with valid inputs **Negative Test Cases:** 1.Create Razorpay Payment Gateway with invalid inputs 2.Create Paytm Payment Gateway with invalid inputs 3. Create Razorpay Payment Gateway without db connection  4.Create Paytm Payment Gateway without db connection| **name** :1.valid characters 2. length>3 and length<64 3.null **descr** :1.valid characters[a-zA-Z0-9 :/-.]2. length>6 and length<256 3.null **mobile** :1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null  **pgSupportContact** :1.Valid Characters 2.length>=10 and length<=13 3.null  **email** :1.valid characters 2.null  **pgtype** **pgVendorType** **pgWebsite** :1.null **pgLogo** :1.null **pgMid** :1.null **pgMkey** :1.null **pgCurrency** **pgCallbackurl** **pgPaymentMethods** :1.null **merchantLogo** :1.null **merchantName** :1.valid characters[a-zA-Z0-9 :/-.]2. length>3 and length<64 3.null **merchantDescr** :1.valid characters[a-zA-Z0-9 :/-.]2. length>6 and length<256 3.null **pytmRequestType** **pytmWebsiteName** **pytmRoot** **pytmFlow** **pytmTokenType** **pytmUrl** :1.null **rzpPartialPayment** :Boolean **serviceCharge** :1.null 2.value<0.1 and value>100 **stateGst** :1.null 2.value<0.1 and value>100 **centralGst** :1.null 2.value<0.1 and value>100|6|10|16|testPosAuthorisedUserCreateRazorpayPaymentGatewayWithValidInputs,  testNegAuthorisedUserCreateRazorpayPaymentGatewayWithInvalidInputs,  testPosAuthorisedUserCreatePaytmPaymentGatewayWithValidInputs,  testNegAuthorisedUserCreatePaytmPaymentGatewayWithInvalidInputs,  testNegCreateRazorpayPaymentGatewayWithoutDBconnection,  testNegCreatePaytmPaymentGatewayWithoutDBconnection|
|1.0| Update Form |ut_p_u_GSTS_WEB_PAYMENT_GATEWAY_470   ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_480   ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_490 |**Positive Test Cases:** Open Payment Gateway update form with valid Id   **Negative Test Cases:**  1.Open Payment Gateway Update Form Without DB Connection 2. Open Payment Gateway Update Form with Invalid id |Id|1|2|3|testPosAuthorisedUserOpenPaymentGatewayUpdateFormWithValidId,  testNegAuthorisedUserOpenPaymentGatewayUpdateFormWithoutDBConnection,  testNegAuthorisedUserOpenPaymenGatewayUdpateFormWithInValidId|
|1.0| Update |ut_p_u_GSTS_WEB_PAYMENT_GATEWAY_500  ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_510   ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_520 ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_635  |**Positive Test Cases:** Update Paytm Payment Gateway with valid inputs    **Negative Test Cases:** 1.  Update Paytm Payment Gateway with Invalid inputs   2. updating without db connection  3.Update already removed Payment Gateway|**updateComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|3|4|testPosAuthorisedUserUpdatePaytmGatewayWithValidInputs,  testAuthorisedUserUpdatePaytmPaymentGatewayWithInvalidInputs,  testNegUpdatePaymentGatewayWithoutDbConnection, testNegAuthorisedUserUpdateAlreadyRemovedPaymentGateway|
|1.0| Remove Form |ut_p_r_GSTS_WEB_PAYMENT_GATEWAY_560   ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_570   ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_580 ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_630|**Positive Test Cases:** Open Payment Gateway remove Form with valid Id    **Negative Test Cases:**  1.Open Payment Gateway remove Form Without DB Connection 2. Open Payment Gateway remove Form with Invalid id   3.Open Payment Gateway remove form with Already removed Payment Gateway Id with Authorised user|Id|1|3|4|testPosAuthorisedUserOpenPaymentGatewayRemoveFormWithValidId,  testNegAuthorisedUserOpenPaymentGatewayRemoveFormWithoutDBConnection,  testNegAuthorisedUserOpenPaymentGatewayRemoveFormWithInValidId,  testNegAuthorisedUserOpenPaymentGatewayRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_PAYMENT_GATEWAY_590  ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_600 ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_610 ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_620 ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_640 |**Positive Test Cases:** Removing Paytm Payment Gateway with valid remove comment   **Negative Test Cases:** 1. Remove Paytm Payment Gateway with InValid Remove Comment 2. Remove Payment Gateway without DB connection  3. Remove already removed Payment Gateway with Authorised User 4. Remove Payment Gateway with invalid id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosAuthorisedUserRemovePaytmPaymentGatewayWithValidRemoveCommentAndValidId,  testNegAuthorisedUserRemovePaytmPaymentGatewayWithInValidRemoveCommentAndValidId,  testNegRemovePaymentGatewayWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedPaymentGateway,  testNegAuthorisedUserRemovePaymentGatewayWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_PAYMENT_GATEWAY_200 ut_n_v_GSTS_WEB_PAYMENT_GATEWAY_210 ut_n_v_GSTS_WEB_PAYMENT_GATEWAY_220 |**Positive Test Cases:** View Payment Gateway Account with Valid Id with Authorised User**Negative Test Cases:** 1.without db connection 2. View Payment Gateway Account with Invalid ID  with Authorised User|1.Valid Id 2.Invalid Id|1|2|3|testPosAuthorisedUserViewPaymentGatewayWithValidId,  testNegAuthorisedUserViewPaymentGatewayWithoutDbConnection,  testNegAuthorisedUserViewPaymentGatewaywithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_PAYMENT_GATEWAY_270 ut_n_s_GSTS_WEB_PAYMENT_GATEWAY_280 ut_n_s_GSTS_WEB_PAYMENT_GATEWAY_290 |**Positive Test Cases:** Search Payment Gateway Account with valid inputs **Negative Test Cases:** 1.Search without db connection  2.Search Payment Gateway Account with Authorised User|  **name:** 1.valid characters 2.length>3 and length<64 **pgVendorType:** Enum values|1|2|3|testPosAuthorisedUserSearchPaymentGatewayWithValidInputs,  testNegAuthorisedUserSearchPaymentGatewayWithoutDBconnection,  testNegAuthorisedUserSearchPaymentGatewayWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_PAYMENT_GATEWAY_240 ut_n_l_GSTS_WEB_PAYMENT_GATEWAY_250 |**Positive Test Cases:** Get Payment Gateway List with Authorised User **Negative Test Cases:** Get Payment Gateway List without db connection||1|1|2|testPosAuthorisedUserGetPaymentGatewayList,  testNegAuthorisedUserPaymentGatewayListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_310   ut_n_ep_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_320   ut_n_ep_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_330 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPaymentGatewayPdfWithValidId,  testNegAuthorisedUserExportPaymentGatewayPdfwithoutDbconnection,  testNegAuthorisedUserExportPaymentGatewayPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_340   ut_n_elp_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_350   ut_n_elp_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_360 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportPaymentGatewayListPdfWithValidId,  testNegAuthorisedUserExportPaymentGatewayListPdfwithoutDbconnection,  testNegAuthorisedUserExportPaymentGatewayListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_370   ut_n_ex_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_380   ut_n_ex_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_390 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportPaymentGatewayXlxWithValidId,  testNegAuthorisedUserExportPaymentGatewayXlxwithoutDbconnection,  testNegAuthorisedUserExportPaymentGatewayXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_400   ut_n_elx_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_410   ut_n_elx_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_420 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPaymentGatewayListXlxWithValidId,  testNegAuthorisedUserExportPaymentGatewayListXlxwithoutDbconnection,  testNegAuthorisedUserExportPaymentGatewayListXlxInValidId|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----| 
|1.0| Create | ut_n_c_GSTS_WEB_PAYMENT_GATEWAY_190  ut_n_c_GSTS_WEB_PAYMENT_GATEWAY_195|1.Create Razorpay Payment Gateway with UnAuthorised User   2.Create Paytm Payment Gateway with UnAuthorised User| **name** :1.valid characters 2. length>3 and length<64 3.null **descr** :1.valid characters[a-zA-Z0-9 :/-.]2. length>6 and length<256 3.null **mobile** :1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null  **pgSupportContact** :1.Valid Characters 2.length>=10 and length<=13 3.null  **email** :1.valid characters 2.null  **pgtype** **pgVendorType** **pgWebsite** :1.null **pgLogo** :1.null **pgMid** :1.null **pgMkey** :1.null **pgCurrency** **pgCallbackurl** **pgPaymentMethods** :1.null **merchantLogo** :1.null **merchantName** :1.valid characters[a-zA-Z0-9 :/-.]2. length>3 and length<64 3.null **merchantDescr** :1.valid characters[a-zA-Z0-9 :/-.]2. length>6 and length<256 3.null **pytmRequestType** **pytmWebsiteName** **pytmRoot** **pytmFlow** **pytmTokenType** **pytmUrl** :1.null **rzpPartialPayment** :Boolean **serviceCharge** :1.null 2.value<0.1 and value>100 **stateGst** :1.null 2.value<0.1 and value>100 **centralGst** :1.null 2.value<0.1 and value>100|0|2|2|testNegUnAuthorisedUserCreateRazorpayPaymentGateway,  testNegUnAuthorisedUserCreatePaytmPaymentGateway|
|1.0| Update Form|ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_550|Unauthorised User opening payment gateway update form||0|1|1|testNegUnAuthorisedUserOpenPaymentGatewayUpdateForm|
|1.0|Update| ut_n_u_GSTS_WEB_PAYMENT_GATEWAY_540 |Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserUpdatePaymentGateway|
|1.0| Remove Form|ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_650|Unauthorised User opening payment gateway remove form||0|1|1|testNegUnAuthorisedUserOpenPaymentGatewayRemoveForm|
|1.0|Remove| ut_n_r_GSTS_WEB_PAYMENT_GATEWAY_660 |Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemovePaymentGateway|
|1.0| View |ut_n_v_GSTS_WEB_PAYMENT_GATEWAY_230 |Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewPaymentGateway|
|1.0| Search |ut_n_s_GSTS_WEB_PAYMENT_GATEWAY_300|Unauthorised User does not have permission to search|  **name:** 1.valid characters 2.length>=3 and length<=64 **pgVendorType:** Enum values|0|1|1|testNegUnAuthorisedUserSearchPaymentGateway|
|1.0| List |ut_n_l_GSTS_WEB_PAYMENT_GATEWAY_260 |Unauthorised User does not have permission to list|Validating with unique field|0|1|1|testNegUnAuthorisedUserGetPaymentGatewayList|
|1.0| PDF |ut_n_ep_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_430 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPaymentGatewayPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_440 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPaymentGatewayListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_450 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPaymentGatewayXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_PAYMENT_GATEWAY_ACCOUNT_460 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPaymentGatewayListXlxWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|


## Security compliance check
1. Only user having the permission **ROLE_PAYMENT_VIEW** should view this functionality 
1. Only user having the permission **ROLE_PAYMENT_CREATE** should create this functionality
1. Only user having the permission **ROLE_PAYMENT_UPDATE** should update this functionality
1. Only user having the permission **ROLE_PAYMENT_REMOVE** should remove this functionality
1. Only user having the permission **ROLE_PAYMENT_VIEW** should export this functionality
1. Only user having the permission **ROLE_PAYMENT_VIEW** should List this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Payment Gateway in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
