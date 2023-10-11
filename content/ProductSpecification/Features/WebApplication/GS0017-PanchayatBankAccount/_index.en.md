---
title: GS0017 - Panchayat Bank Account
tags : ["Composing"]
---

## Introduction
Panchayat bank account is one of the features of our software product. Panchayat bank account holds the information of bank account details that belongs to a panchayat. When a user makes a tax payment the amount is transferred to a fixed account. The transactions which were made to a fixed account on each day are again transferred to the taxpayer's panchayat bank account on the night of the same day.

## Business Assumptions
Creating and removing the panchayat bank account can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Users should create, remove or view the panchayat bank account at only panchayat level.
1. Any level of users can create, remove or view the panchayat bank account.
1. Each panchayat contain only one active panchayat bank account at a given time.
1. Creation of bank account is not possible in selected panchayat when there is active bank account available.
1. Each bank account has unique account number.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access panchayat bank accounts.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Panchayat bank account feature contains the information of bank details belongs to a panchayat. 

### Design 
1. Each panchayat bank account contains account number, ifsc, micr, bank, name and description.
1. We can create, view, and remove the panchayat bank account.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_panchayat_bank_account_create|To create the panchayat bank account|
|uc_panchayat_bank_account_remove|To remove the panchayat bank account|
|uc_panchayat_bank_account_view|To view the panchayat bank account|
|uc_panchayat_bank_account_search|To search the panchayat bank account|
|uc_panchayat_bank_account_export|To export the panchayat bank account in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Account Number|YES|NA|Allowed 0-9, maxlen=18 |@Column(name = "accNumber", length = 32, nullable = false, unique = true)|accNumber varchar(32) not null|YES|-|YES|YES|YES|NO||
|IFSC|YES|NA|Allowed A-Z, 0-9, maxlen=11|@Column(name = "ifsc ", length = 32, nullable = false)|ifsc varchar(32) not null|YES|-|YES|YES|NO|NO||
|MICR|NO|NA|Allowed 0-9, maxlen=9 |@Column(name = "micr", length = 32, nullable = true)|micr varchar(32) default null|YES|-|YES|YES|NO|NO||
|Bank|YES|NA|Drop Down List|@Enumerated(EnumType.STRING) @Column(name = "bank ", length = 64, nullable = false)|bank varchar(32) not null|YES|-|YES|YES|YES|YES||
|Name|YES|NA|Allowed a-z, A-Z, 0-9, space|@Column(name = "name", length = 64, nullable = false)|name varchar(64) not null|YES|-|YES|YES|YES|YES||
|Description|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . , # , : , / and comma and length 6 to 256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) not null|YES|-|YES|YES|YES|NO||
|Removed Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . , # , : , / and comma and length 6 to 255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|-|YES|YES|NO|NO||

#### Enum Constants

##### Bank

{{<mermaid align="left">}}
classDiagram
    class Name{
    ALLAHABAD_BANK,
	ANDHRA_BANK,
	AXIS_BANK,
	BANK_OF_BAHRAIN_AND_KUWAIT,
	BANK_OF_BARODA_CORPORATE_BANKING,
	BANK_OF_BARODA_RETAIL_BANKING,
	BANK_OF_INDIA,
	BANK_OF_MAHARASHTRA,
	CANARA_BANK,
	CENTRAL_BANK_OF_INDIA,
	CITY_UNION_BANK,
	CORPORATION_BANK,
	DEUTSCHE_BANK,
	DEVELOPMENT_CREDIT_BANK,
	DHANLAXMI_BANK,
	FEDERAL_BANK,
	ICICI_BANK,
	IDBI_BANK,
	INDIAN_BANK,
	INDIAN_OVERSEAS_BANK,
	INDUSIND_BANK,
	ING_VYSYA_BANK,
	JAMMU_AND_KASHMIR_BANK,
	KARNATAKA_BANK_LTD,
	KARUR_VYSYA_BANK,
	KOTAK_BANK,
	LAXMI_VILAS_BANK,
	ORIENTAL_BANK_OF_COMMERCE,
	PUNJAB_NATIONAL_BANK_CORPORATE_BANKING,
	PUNJAB_NATIONAL_BANK_RETAIL_BANKING,
	PUNJAB_AND_SIND_BANK,
	SHAMRAO_VITTHAL_COOPERATIVE_BANK,
	SOUTH_INDIAN_BANK,
	STATE_BANK_OF_BIKANER_AND_JAIPUR,
	STATE_BANK_OF_HYDERABAD,
	STATE_BANK_OF_INDIA,
	STATE_BANK_OF_MYSORE,
	STATE_BANK_OF_PATIALA,
	STATE_BANK_OF_TRAVANCORE,
	SYNDICATE_BANK,
	TAMILNAD_MERCANTILE_BANK_LTD,
	UCO_BANK,
	UNION_BANK_OF_INDIA,
	UNITED_BANK_OF_INDIA,
	VIJAYA_BANK,
	YES_BANK_LTD;
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|PANCHAYAT_BANK_ACCOUNT_CREATE|Create|
|PANCHAYAT_BANK_ACCOUNT_REMOVE|Remove|
|PANCHAYAT_BANK_ACCOUNT_VIEW|View|
|PANCHAYAT_BANK_ACCOUNT_VIEW|List|
|PANCHAYAT_BANK_ACCOUNT_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_pb_acc__account_number (account_number)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_panchayat_bank_account_create|Only user having the permission to create, should create this functionality|
|ac_panchayat_bank_account_remove|Only user having the permission to remove, should remove this functionality|
|ac_panchayat_bank_account_view|Only user having the permission to view, should view this functionality|
|ac_panchayat_bank_account_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreteBtn[Create]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	PanchayatBankAccountMenu((Panchayat Bank Account Menu))
	ListPage{Panchayat Bank Account List Page}
	CreatePage((Create Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->PanchayatBankAccountMenu
    subgraph Menu
    PanchayatBankAccountMenu
	end
	subgraph List
	PanchayatBankAccountMenu-->ListPage
	ListPage--C-R-V-E-->ListPage
	end
	subgraph Error
	PanchayatBankAccountMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph Create
	ListPage--C-->CreatePage
	CreatePage--SB-->ListPage
	CreatePage--SB-->CreatePage
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
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
	
{{</mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|Create|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|C-R-V-E|Create or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram
1. Only a user with the PANCHAYAT_BANK_ACCOUNT_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant PanchayatBankAccountListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet, GET /app/ctx/PanchayatBankAccount/list ListPage
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S:  GET /app/ctx/PanchayatBankAccount/list ListPage
        cloud-->>-PanchayatBankAccountListPage: RES:List Page
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet, GET /app/PanchayatBankAccount/create/form CreateFormPage
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S : GET /app/PanchayatBankAccount/create/form CreateFormPage
        cloud-->>-PanchayatBankAccountListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: POST /app/PanchayatBankAccount/create Create
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S : POST /app/PanchayatBankAccount/create Create
        cloud-->>-PanchayatBankAccountListPage: RES: An Panchayat Bank Account Successfully Created
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: GET /app/PanchayatBankAccount/remove/form RemoveFormPage
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S : GET /app/PanchayatBankAccount/remove/form RemoveFormPage
        cloud-->>-PanchayatBankAccountListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: POST /app/PanchayatBankAccount/remove Remove
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S : POST /app/PanchayatBankAccount/remove Remove
        cloud-->>-PanchayatBankAccountListPage: RES: A Panchayat Bank Account Successfully Removed
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: GET /app/PanchayatBankAccount/view ViewPage
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        alt
        Note right of Net: Panchayat Bank Account Cache Object Found
        PanchayatBankAccountListPage->>+Cache: S : GET /app/PanchayatBankAccount/view ViewPage
        Cache-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount View
        else
        Note right of Net: Panchayat Bank Account Cache Object Not Found
        Cache->>+cloud: GET /app/PanchayatBankAccount/view ViewPage
        cloud-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount View
        end
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: GET /app/PanchayatBankAccount/exportPdf ExportPdf
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        alt
        Note right of Net: Panchayat Bank Account Cache Object Found
        PanchayatBankAccountListPage->>+Cache: S : GET /app/PanchayatBankAccount/exportPdf ExportPdf
        Cache-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount Pdf
        else
        Note right of Net: Panchayat Bank Account Cache Object Not Found
        Cache->>+cloud: GET /app/PanchayatBankAccount/exportPdf ExportPdf
        cloud-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount Pdf
        end
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: GET /app/PanchayatBankAccount/exportListPdf ExportListPdf
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S : GET /app/PanchayatBankAccount/exportListPdf ExportListPdf
        cloud-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount List Pdf
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: GET /app/PanchayatBankAccount/exportXlx ExportXlx
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        alt
        Note right of Net: Panchayat Bank Account Cache Object Found
        PanchayatBankAccountListPage->>+Cache: S : GET /app/PanchayatBankAccount/exportXlx ExportXlx
        Cache-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount Xlx
        else
        Note right of Net: Panchayat Bank Account Cache Object Not Found
        Cache->>+cloud: GET /app/PanchayatBankAccount/exportXlx ExportXlx
        cloud-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount Xlx
        end
    end
    rect rgb(244,244,244)
        PanchayatBankAccountListPage->>+Net: Check Internet: GET /app/PanchayatBankAccount/exportListXlx ExportListXlx
        Net--x-PanchayatBankAccountListPage: F : Connection Error
        PanchayatBankAccountListPage->>+cloud: S : GET /app/PanchayatBankAccount/exportListXlx ExportListXlx
        cloud-->>-PanchayatBankAccountListPage: RES: panchayatBankAccount List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|------------------|--------------------------|-------------------------|----------------|--------|
|1.0| Create Form |ut_p_c_GSTS_WEB_BANKACCOUNT_120 ut_n_c_GSTS_WEB_BANKACCOUNT_130 ut_n_c_GSTS_WEB_BANKACCOUNT_920 |**Positive Test Cases:** Open Bank Account Create Form at panchayat level with Authorised User   **Negative Test Cases:** 1.Open Bank Account Create Form Without Db connection   2. Open Bank Account Create Form when One Active bank account already exists in the same panchayat|-|1|2|3|testPosOpenBankAccountCreateFormAtPanLevelWithAuthorisedUser,  testNegOpenBankAccountCreateFormWithoutDBConnection,  testPosOpenBankAccountCreateFormWhenActiveBankAccountExists|
|1.0| Create |ut_p_c_GSTS_WEB_BANKACCOUNT_150  ut_n_c_GSTS_WEB_BANKACCOUNT_160 ut_n_c_GSTS_WEB_BANKACCOUNT_140 ut_n_c_GSTS_WEB_BANKACCOUNT_910 |**Positive Test Cases:**   Creating Bank Account at panchayat level with Authorised User   **Negative Test Cases:**   1.Creating Bank Account with invalid inputs   2. Create Bank Account without db connection   3.Create Bank Account when One Active bank account already exists in the same panchayat|**accNumber:**  1.valid characters 2.length>=6 and length<=18 3.null **ifsc:** 1.valid characters 2.length == 11 3.null  **micr:** 1.valid characters 2. length == 9 3. null **bank:** 1.enums 2.null **name:** 1.valid characters 2. length>=6 and length<=18 3. null **descr:** 1.valid characters 2.length>=6 and length<=256 3.null|48|5|53|testPosAuthorisedUserCreateBankAccountAtPanchayatLevel,  testNegAuthorisedPanchayatLevelUserCreateBankAccountWithInValidInputs,  testNegCreateBankAccountWithoutDBconnection,  testPosCreateBankAccountWhenActiveBankAccountExists|
|1.0| Remove Form |ut_p_r_GSTS_WEB_BANKACCOUNT_930   ut_n_r_GSTS_WEB_BANKACCOUNT_940   ut_n_r_GSTS_WEB_BANKACCOUNT_950 ut_n_r_GSTS_WEB_BANKACCOUNT_1080|**Positive Test Cases:** Open bank account remove Form with valid Id at panchayat level   **Negative Test Cases:**  1.Open bank account remove Form Without DB Connection   2. Open bank account remove Form with Invalid id   3.Open bank account remove form with Already removed bank account Id with Authorised user|Id|1|3|4|testPosAuthorisedUserOpenBankAccountRemoveFormWithValidIdAtPanLevel,  testNegAuthorisedPanLevelUserOpenBankAccountRemoveFormWithoutDBConnection,  testNegAuthorisedUserOpenBankAccountRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenBankAccountRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_BANKACCOUNT_1030  ut_n_r_GSTS_WEB_BANKACCOUNT_1040 ut_n_r_GSTS_WEB_BANKACCOUNT_1050 ut_n_r_GSTS_WEB_BANKACCOUNT_1060 ut_n_r_GSTS_WEB_BANKACCOUNT_1070 |**Positive Test Cases:** Removing bank account with valid remove comment at Panchayat Level  **Negative Test Cases:** 1. Remove bank account with InValid Remove Comment 2. Remove  bank account without DB connection  3. Remove bank account with invalid id 4.  Remove already removed bank account with Authorised User| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosAuthorisedUserRemoveBankAccountWithValidRemoveCommentAndValidIdAtPanchayatLevel,  testPosAuthorisedUserRemoveBankAccountWithInValidRemoveCommentAndValidId,  testNegRemoveBankAccountWithoutDbConnection,  testNegAuthorisedUserRemoveBanAccountWithInValidId, testNegAuthorisedUserRemoveAlreadyBankAccount|
|1.0| View |ut_p_v_GSTS_WEB_BANKACCOUNT_230  ut_n_v_GSTS_WEB_BANKACCOUNT_240 ut_n_v_GSTS_WEB_BANKACCOUNT_250 |**Positive Test Cases:** View Bank Account with Valid Id at Panchayat Level   **Negative Test Cases:** 1.without db connection   2.View Bank Account with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewBankAccountWithValidIdAtPanchayatLevel,  testNegAuthorisedUserViewBankAccountWithoutDbConnection,  testNegAuthorisedUserViewBankAccountwithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_BANKACCOUNT_310 utn_s_GSTS_WEB_BANKACCOUNT_320 ut_n_s_GSTS_WEB_BANKACCOUNT_330|**Positive Test Cases:** Search Bank Account with valid inputs at panchayat Level **Negative Test Cases:** 1.without db connection 2.Search Bank Account with invalid inputs|**1.bank 2.name**|3|1|4|testPosAuthorisedUserSearchBankAccountWithValidInputsAtPanchayatLevel,  testNegAuthorisedUserSearchBankAccountWithoutDBconnection,  testNegAuthorisedUserSearchBankAccountWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_BANKACCOUNT_350 ut_n_l_GSTS_WEB_BANKACCOUNT_360|**Positive Test Cases:** Get Bank Account List at Panchayat Level **Negative Test Cases:** Without db connection||1|2|3|testPosAuthorisedUserGetBankAccountListAtPanchayatLevel,  testNegAuthorisedUserBankAccountListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_BANKACCOUNT_710   ut_n_ep_GSTS_WEB_BANKACCOUNT_720   ut_n_ep_GSTS_WEB_BANKACCOUNT_730 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportBankAccountPdfWithValidId,  testNegAuthorisedUserExportBankAccountPdfwithoutDbconnection,  testNegAuthorisedUserExportBankAccountPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_BANKACCOUNT_740   ut_n_elp_GSTS_WEB_BANKACCOUNT_750   ut_n_elp_GSTS_WEB_BANKACCOUNT_760 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportBankAccountListPdfWithValidId,  testNegAuthorisedUserExportBankAccountListPdfwithoutDbconnection,  testNegAuthorisedUserExportBankAccountListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_BANKACCOUNT_770   ut_n_ex_GSTS_WEB_BANKACCOUNT_780   ut_n_ex_GSTS_WEB_BANKACCOUNT_790 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportBankAccountXlxWithValidId,  testNegAuthorisedUserExportBankAccountXlxwithoutDbconnection,  testNegAuthorisedUserExportBankAccountXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_BANKACCOUNT_800   ut_n_elx_GSTS_WEB_BANKACCOUNT_810   ut_n_elx_GSTS_WEB_BANKACCOUNT820 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportBankAccountListXlxWithValidId,  testNegAuthorisedUserExportBankAccountListXlxwithoutDbconnection,  testNegAuthorisedUserExportBankAccountListXlxInValidId|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|--------------------|----|
|1.0| Create |ut_n_c_GSTS_WEB_BANKACCOUNT_210 |Unauthorised User does not have permission to create|**accNumber:**  1.valid characters 2.length>=6 and length<=18 3.null **ifsc:** 1.valid characters 2.length == 11 3.null  **micr:** 1.valid characters 2. length == 9 3. null **bank:** 1.enums 2.null **name:** 1.valid characters 2. length>=6 and length<=18 3. null **descr:** 1.valid characters 2.length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserCreateBankAccount|
|1.0| Create Form|ut_n_c_GSTS_WEB_BANKACCOUNT_220|Unauthorised User opening bank account create form||0|1|1|testNegUnAuthorisedUserOpenBankAccountCreateForm|
|1.0| Remove Form|ut_n_r_GSTS_WEB_BANKACCOUNT_960|Unauthorised User opening bank account remove form||0|1|1|testNegUnAuthorisedUserOpenBankAccountRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_BANKACCOUNT_970|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=256 3.null |0|1|1|testNegUnAuthorisedUserRemoveBankAccount|
|1.0| View |ut_n_v_GSTS_WEB_BANKACCOUNT_300|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewBankAccount|
|1.0| Search |ut_n_s_GSTS_WEB_BANKACCOUNT_350|Unauthorised User does not have permission to search|**1.bank 2.name**|0|1|1|testNegUnAuthorisedUserSearchBankAccount|
|1.0| List |ut_n_l_GSTS_WEB_BANKACCOUNT_700|Unauthorised User does not have permission to list||0|1|1|testNegUnAuthorisedUserBankAccountList|
|1.0| PDF |ut_n_ep_GSTS_WEB_BANKACCOUNT_870 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportBankAccountPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_BANKACCOUNT_880 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportBankAccountListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_BANKACCOUNT_890 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportBankAccountXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_BANKACCOUNT_900 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportBankAccountListXlxWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|--------|
|1.0|Create|ut_n_c_GSTS_WEB_BANKACCOUNT_170|Create Bank Account at State Level with Authorised User| N/A |Will not be Created|1|testNegCreateBankAccountAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_BANKACCOUNT_180|Create Bank Account at District Level with Authorised User| N/A |Will not be Created|1|testNegCreateBankAccountAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_BANKACCOUNT_190|Create Bank Account at Division Level with Authorised User| N/A |Will not be Created|1|testNegCreateBankAccountAtDivisionLevel|
|1.0|Create|ut_n_c_GSTS_WEB_BANKACCOUNT_200|Create Bank Account at Mandal Level with Authorised User| N/A |Will not be Created|1|testNegCreateBankAccountAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_BANKACCOUNT_260|Authorised User Viewing Bank Account at State Level| N/A |Will not be Accessed|1|testNegViewBankAccountAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_BANKACCOUNT_270|Authorised User Viewing Bank Account at District Level| N/A |Will not be Accessed|1|testNegViewBankAccountAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_BANKACCOUNT_280|Authorised User Viewing Bank Account at Division Level| N/A |Will not be Accessed|1|testNegViewBankAccountAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_BANKACCOUNT_290|Authorised User Viewing Bank Account at Mandal Level| N/A |Will not be Accessed|1|testNegViewBankAccountAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_BANKACCOUNT_340|Authorised User search Bank Account at State Level| N/A |Will not be Accessed|1|testNegSearchBankAccountAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_BANKACCOUNT_690|Authorised User Accessing Bank Account list at State Level| N/A |Will not be Accessed|1|testNegBankAccountListAtStateLevel|
|1.0| PDF |ut_n_ep_GSTS_WEB_BANKACCOUNT_830 |Export Pdf at state level|N/A|will not be exported|1|testNegExportBankAccountPdfAtStateLevel|
|1.0| List PDF |ut_n_elp_GSTS_WEB_BANKACCOUNT_840 |Export List Pdf at state level|N/A|will not be exported|1|testNegExportBankAccountListPdfAtStateLevel|
|1.0| XLX |ut_n_ex_GSTS_WEB_BANKACCOUNT_850 |Export xlx at state level|N/A|will not be exported|1|testNegExportBankAccountXlxAtStateLevel|
|1.0| List XLX |ut_n_elx_GSTS_WEB_BANKACCOUNT_860 |Export List xlx at state level|N/A|will not be exported|1|testNegExportBankAccountListXlxAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_BANKACCOUNT_980|Remove Bank Account at State Level with Authorised User| N/A |Will not be Removed|1|testNegAuthorisedUserRemoveBankAccountAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_BANKACCOUNT_990|Remove Bank Account at District Level with Authorised User| N/A |Will not be Removed|1|testNegAuthorisedUserRemoveBankAccountAtDistrictLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_BANKACCOUNT_1000|Remove Bank Account at Division Level with Authorised User| N/A |Will not be Removed|1|testNegAuthorisedUserRemoveBankAccountAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_BANKACCOUNT_1010|Remove Bank Account at Mandal Level with Authorised User| N/A |Will not be Removed|1|testNegAuthorisedUserRemoveBankAccountAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_BANKACCOUNT_1020|Panchayat1112 user trying to remove Panchayat1111 Bank Account which does not belongs to his context| N/A |Will not be Removed|1|testNegPanchayat1112UserRemovingPanchayat1111BankAccount|
|1.0|View|ut_n_v_GSTS_WEB_BANKACCOUNT_1090|Panchayat1112 user trying to access Panchayat1111 Bank Account which does not belongs to his context| N/A |Will not be Accessed|1|testNegPanchayat1112UserAccessingPanchayat1111BankAccount|


## Security compliance check
1. Only user having the user role with permission **ROLE_PANCHAYAT_BANK_ACCOUNT_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_PANCHAYAT_BANK_ACCOUNT_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_PANCHAYAT_BANK_ACCOUNT_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the PANCHAYAT BANK ACCOUNT should be provided in the User Manual.

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




 
