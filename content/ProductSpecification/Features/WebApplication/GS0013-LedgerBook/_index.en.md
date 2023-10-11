---
title: GS0013 - Ledger Book
tags : ["Composing"]
---

## Introduction
Ledger Book is one of the features of this software product. Ledger Book contains all the financial information of panchayat. Every panchayat has its own ledger book. Users will have access to ledger book if they have permission, Otherwise will not access. 

## Business Assumptions
what type of users can create ledger entry in ledger book should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the ledger entry in ledger book.  
1. Ledger Book feature is accessible at panchayat level only.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access ledger book.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Ledger Book contains information about all financial activites happend in panchayat.

### Design 
1. Each Ledger Entry in Ledger book has Work Type, Ledger Date, Amount,  Govt Order Number,  Panchayat Resolution Number, Description and Attachment. 
1. We can create, remove, view and export the ledger entry.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_ledger_book_list|To view all the ledger entries. This listing page should bind to a permission|
|uc_ledger_book_create|To create the ledger entry. This create page should bind to a permission|
|uc_ledger_book_remove|To remove the ledger entry. This remove page should bind to a permission|
|uc_ledger_book_view|To view the ledger entry. This view page should bind to a permission|
|uc_ledger_book_search|To search the ledger entry. This search page should bind to a permission|
|uc_ledger_book_export|To export the ledger entry in 2 formats Excel, PDF. This Export page should bind to a permission|
 
#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|workType|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "work_type", length = 64, nullable = false)|work_type varchar(64) NOT NULL|YES|YES|YES|YES|YES||
|ledgerDate|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "ledger_date", nullable = false)|ledger_date datetime NOT NULL|YES|YES|YES|YES|YES||
|amount|YES|NA|0-9 and ., maxlen=10|@Column(name = "amount", nullable = false)|amount float(16,2) NOT NULL|YES|YES|YES|YES|YES||
|govtOrderNumber|NO|NA|Drop Down Values|@Column(name = "go_no", length = 32, nullable = true)|go_no varchar(32) DEFAULT NULL|YES|YES|YES|YES|YES||
|panchayatResolutionNumber|NO|NA|Drop Down Values|@Column(name = "pr_no", length = 32, nullable = true)|pr_no VARCHAR(32) DEFAULT NULL|YES|YES|YES|NO|YES||
|descr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|YES|YES|YES|NO||
|fileName|YES|NA|Attachment|@Column(name = "file_name", length = 36, nullable = false)|file_name varchar(36) NOT NULL|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Work Type

{{<mermaid align="left">}}
classDiagram
    class WorkType{
      PURCHASE
      ADVANCE
      TRACTOR
      AUTO_RICKSHAW
      NONE
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

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|||
## User Experience
1. Create page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	LedgerBookMenu((Ledger Book Menu))
	ListPage{Ledger Book List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->LedgerBookMenu
    subgraph Menu
    LedgerBookMenu
    end
    subgraph   
    LedgerBookMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    LedgerBookMenu--F-->ErrorPage
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
|S|Submit|
|B|Back|
|SB|Submit or Back|
|C-R-V-E|Create or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram


{{<mermaid align="center">}}
sequenceDiagram
    participant LedgerBookListpage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet, GET /app/ctx/LedgerBook/list ListPage
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S:  GET /app/ctx/LedgerBook/list ListPage
        cloud-->>-LedgerBookListpage: RES:List Page
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet, GET /app/LedgerBook/create/form CreateFormPage
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : GET /app/LedgerBook/create/form CreateFormPage
        cloud-->>-LedgerBookListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: POST /app/LedgerBook/create Create
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : POST /app/LedgerBook/create Create
        cloud-->>-LedgerBookListpage: RES: An LedgerBook Successfully Created
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/remove/form RemoveFormPage
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : GET /app/LedgerBook/remove/form RemoveFormPage
        cloud-->>-LedgerBookListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: POST /app/LedgerBook/remove Remove
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : POST /app/LedgerBook/remove Remove
        cloud-->>-LedgerBookListpage: RES: An LedgerBook Successfully Removed
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/view ViewPage
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: GET /app/LedgerBook/view ViewPage
        cloud-->>-LedgerBookListpage: RES: LedgerBook View
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/exportPdf ExportPdf
        Net--x-LedgerBookListpage: F : Connection Error 
        LedgerBookListpage->>+cloud: GET /app/LedgerBook/exportPdf ExportPdf
        cloud-->>-LedgerBookListpage: RES: LedgerBook Pdf
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/exportListPdf ExportListPdf
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : GET /app/LedgerBook/exportListPdf ExportListPdf
        cloud-->>-LedgerBookListpage: RES: LedgerBook List Pdf
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/exportXlx ExportXlx
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: GET /app/LedgerBook/exportXlx ExportXlx
        cloud-->>-LedgerBookListpage: RES: LedgerBook Xlx
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/exportListXlx ExportListXlx
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : GET /app/LedgerBook/exportListXlx ExportListXlx
        cloud-->>-LedgerBookListpage: RES: LedgerBook List Xlx
    end
    rect rgb(244,244,244)
        LedgerBookListpage->>+Net: Check Internet: GET /app/LedgerBook/download DownloadCopy
        Net--x-LedgerBookListpage: F : Connection Error
        LedgerBookListpage->>+cloud: S : GET /app/LedgerBook/download DownloadCopy
        cloud-->>-LedgerBookListpage: RES: LedgerBook Copy
    end
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-------|
|1.0| Create Form |ut_p_c_GSTS_WEB_LEDGERBOOK_120 ut_n_c_GSTS_WEB_LEDGERBOOK_130 |**Positive Test Cases:** 1.Open Ledger Entry Create Form At panchayat level  **Negative Test Cases:** Open Ledger Entry Create Form Without Db connection|-|1|1|2|testPosOpenLedgerEntryCreateFormAtPanLevelWithAuthorisedUser,  testNegOpenLedgerEntryCreateFormWithoutDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_LEDGERBOOK_150  ut_n_c_GSTS_WEB_LEDGERBOOK_160 ut_n_c_GSTS_WEB_LEDGERBOOK_140 |**Positive Test Cases:** Create Ledger Entry with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1.Create Ledger Entry with Invalid Inputs 2.Create Ledger Entry without db connection|**workType:** enums **amount:** 1.null 2. value >0 **descr:** 1.valid characters 2.length>=6 and length<=256 3.null **govtOrderNumber:** drop down values **panchayatResolutionNumber:** drop down values **ledgerDate:** 1.null 2.valid Date **fileName:** file upload|6|9|15|testPosAuthorisedPanchayatLevelUserCreateLedgerEntryWithValidInputs,  testNegAuthorisedPanchayatLevelUserCreateLedgerEntryWithInValidInputs,  testNegCreateLedgerEntryWithoutDBconnection|
|1.0| Create |ut_n_c_GSTS_WEB_LEDGERBOOK_165  |**Negative Test Cases:** Create Ledger Entry without File Attachment |-|0|1|1|testNegCreateLedgerEntryWithoutFileAttachment|
|1.0| Remove Form |ut_p_r_GSTS_WEB_LEDGERBOOK_380   ut_n_r_GSTS_WEB_LEDGERBOOK_390   ut_n_r_GSTS_WEB_LEDGERBOOK_400  ut_n_r_GSTS_WEB_LEDGERBOOK_460|**Positive Test Cases:** Open Ledger Entry remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Ledger Entry remove Form Without DB Connection 2. Open Ledger Entry remove Form with Invalid id   3.Open Ledger Entry remove form with Already removed Ledger Entry Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelLedgerEntryRemoveFormWithValidId,  testNegAuthorisedPanLevelUserOpenLedgerEntryRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenLedgerEntryRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenLedgerEntryRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_LEDGERBOOK_410  ut_n_r_GSTS_WEB_LEDGERBOOK_420 ut_n_r_GSTS_WEB_LEDGERBOOK_440  ut_n_r_GSTS_WEB_LEDGERBOOK_450 |**Positive Test Cases:** Remove Ledger Entry with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Ledger entry with invalid remove comment 2.Remove Ledger Entry without db connection 3.Remove already removed Ledger Entry| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|3|4|testPosPanLevelAuthorisedUserRemoveLedgerEntryWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveLedgerEntryWithInValidRemoveCommentAndValidId,  testNegRemoveLedgerEntryWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedLedgerEntry|
|1.0| View |ut_p_v_GSTS_WEB_LEDGERBOOK_590  ut_n_v_GSTS_WEB_LEDGERBOOK_600 ut_n_v_GSTS_WEB_LEDGERBOOK_610 |**Positive Test Cases:** View Ledger entry with Valid Id  with Authorised User **Negative Test Cases:** 1.View Ledger Entry without db connection 2.View Ledger entry  with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewLedgerEntryWithValidId,  testNegAuthorisedUserViewLedgerEntryWithoutDbConnection,  testNegAuthorisedUserViewLedgerEntrywithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_LEDGERBOOK_740 ut_n_s_GSTS_WEB_LEDGERBOOK_750 ut_n_s_GSTS_WEB_LEDGERBOOK_760|**Positive Test Cases:**  Search Ledger Entry with valid inputs **Negative Test Cases:** 1.Search Ledger Entry without db connection 2.Search Ledger Entry with invalid Inputs|**1.workType 2.descr 3.govtOrderNumber 4.panchayatResolutionNumber 5.ledgerDate 6.amount**|7|2|9|testPosAuthorisedUserSearchLedgerEntryWithValidInputs,  testNegAuthorisedUserSearchLedgerEntryWithoutDBconnection,  testNegAuthorisedUserSearchLedgerEntryWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_LEDGERBOOK_670 ut_n_l_GSTS_WEB_LEDGERBOOK_680|**Positive Test Cases:** Get Ledger Entry List with Authorised User **Negative Test Cases:** Get Ledger Entry List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserGetLedgerEntryList,  testNegAuthorisedUserLedgerEntryListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_LEDGERBOOK_810   ut_n_ep_GSTS_WEB_LEDGERBOOK_820   ut_n_ep_GSTS_WEB_LEDGERBOOK_830 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportLedgerEntryPdfWithValidId,  testNegAuthorisedUserExportLedgerEntryPdfwithoutDbconnection,  testNegAuthorisedUserExportLedgerEntryPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_LEDGERBOOK_840   ut_n_elp_GSTS_WEB_LEDGERBOOK_850   ut_n_elp_GSTS_WEB_LEDGERBOOK_860 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportLedgerEntryListPdfWithValidId,  testNegAuthorisedUserExportLedgerEntryListPdfwithoutDbconnection,  testNegAuthorisedUserExportLedgerEntryListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_LEDGERBOOK_870   ut_n_ex_GSTS_WEB_LEDGERBOOK_880   ut_n_ex_GSTS_WEB_LEDGERBOOK_890 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportLedgerEntryXlxWithValidId,  testNegAuthorisedUserExportLedgerEntryXlxwithoutDbconnection,  testNegAuthorisedUserExportLedgerEntryXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_LEDGERBOOK_900   ut_n_elx_GSTS_WEB_LEDGERBOOK_910   ut_n_elx_GSTS_WEB_LEDGERBOOK_920 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportLedgerEntryListXlxWithValidId,  testNegAuthorisedUserExportLedgerEntryListXlxwithoutDbconnection,  testNegAuthorisedUserExportLedgerEntryListXlxInValidId|
|1.0| Download|ut_p_elx_GSTS_WEB_LEDGERBOOK_930   ut_n_elx_GSTS_WEB_LEDGERBOOK_940   ut_n_elx_GSTS_WEB_LEDGERBOOK_950 |**Positive Test Cases:** Download ledger entry attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.ledger entry attachment with Invalid Id|Id |1|2|3|testPosAuthorisedUserDownloadLedgerEntryAttachmentValidId,  testPosAuthorisedUserDownloadLedgerEntryAttachmentwithoutDbConnection,  testNegAuthorisedUserDownloadLedgerEntryAttachmentInValidId|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----|
|1.0| Create Form|ut_n_c_GSTS_WEB_LEDGERBOOK_260|Unauthorised User opening ledger entry create form||0|1|1|testNegUnAuthorisedUserOpenLedgerEntryCreateForm|
|1.0| Create |ut_n_c_GSTS_WEB_LEDGERBOOK_250|Unauthorised User does not have permission to create|**workType:** enums **amount:** 1.null 2. value >0 **descr:** 1.valid characters 2.length>=6 and length<=256 3.null **govtOrderNumber:** drop down values **panchayatResolutionNumber:** drop down values **ledgerDate:** 1.null 2.valid Date **fileName:** file upload|0|1|1|testNegUnAuthorisedUserCreateLedgerEntry|
|1.0| Remove Form|ut_n_r_GSTS_WEB_LEDGERBOOK_570|Unauthorised User opening ledger entry remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenLedgerEntryRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_LEDGERBOOK_580|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveLedgerEntry|
|1.0| View |ut_n_v_GSTS_WEB_LEDGERBOOK_660|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewLedgerEntry|
|1.0| Search |ut_n_s_GSTS_WEB_LEDGERBOOK_800|Unauthorised User does not have permission to search|**1.workType 2.descr 3.govtOrderNumber 4.panchayatResolutionNumber 5.ledgerDate 6.amount**|0|1|1|testNegUnAuthorisedUserSearchLedgerEntry|
|1.0| List |ut_n_l_GSTS_WEB_LEDGERBOOK_730|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserLedgerEntryList|
|1.0| PDF |ut_n_ep_GSTS_WEB_LEDGERBOOK_1020 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportLedgerEntryPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_LEDGERBOOK_1030 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportLedgerEntryListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_LEDGERBOOK_1040 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportLedgerEntryXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_LEDGERBOOK_1050 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportLedgerEntryListXlxWithValidId|
|1.0| Download |ut_n_elx_GSTS_WEB_LEDGERBOOK_1060 |Download ledger entry attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadLedgerEntryAttachmentWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|----------|
|1.0|Create|ut_n_c_GSTS_WEB_LEDGERBOOK_170|Create Ledger Entry at State Level| N/A |Will not be Created|1|testNegCreateLedgerEntryAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_LEDGERBOOK_180|Open Ledger Entry Create Form at State Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_LEDGERBOOK_190|Create Ledger Entry at District Level| N/A |Will not be Created|1|testNegCreateLedgerEntryAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_LEDGERBOOK_200|Open Ledger Entry Create Form at District Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_LEDGERBOOK_210|Create Ledger Entry at Division Level| N/A |Will not be Created|1|testNegCreateLedgerEntryAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_LEDGERBOOK_220|Open Ledger Entry Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_LEDGERBOOK_230|Create Ledger Entry at Mandal Level| N/A |Will not be Created|1|testNegCreateLedgerEntryAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_LEDGERBOOK_240|Open Ledger Entry Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryCreateFormAtMandalLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_LEDGERBOOK_490|Open Ledger Entry Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_LEDGERBOOK_500|Remove Ledger Entry at State Level| N/A |Will not be Removed|1|testNegRemoveLedgerEntryAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_LEDGERBOOK_510|Open Ledger Entry Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_LEDGERBOOK_520|Remove Ledger Entry at District Level| N/A |Will not be Removed|1|testNegRemoveLedgerEntryAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_LEDGERBOOK_530|Open Ledger Entry Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_LEDGERBOOK_540|Remove Ledger Entry at Division Level| N/A |Will not be Removed|1|testNegRemoveLedgerEntryAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_LEDGERBOOK_550|Open Ledger Entry Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenLedgerEntryRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_LEDGERBOOK_560|Remove Ledger Entry at Mandal Level| N/A |Will not be Removed|1|testNegRemoveLedgerEntryAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_LEDGERBOOK_620|View Ledger Entry at State Level| N/A |Will not be Accessed|1|testNegViewLedgerEntryAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_LEDGERBOOK_630|View Ledger Entry at District Level| N/A |Will not be Accessed|1|testNegViewLedgerEntryAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_LEDGERBOOK_640|View Ledger Entry at Division Level| N/A |Will not be Accessed|1|testNegViewLedgerEntryAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_LEDGERBOOK_650|View Ledger Entry at Mandal Level| N/A |Will not be Accessed|1|testNegViewLedgerEntryAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_LEDGERBOOK_690|Get Ledger Entry List at State Level| N/A |Will not be Accessed|1|testNegLedgerEntryListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_LEDGERBOOK_700|Get Ledger Entry List at District Level| N/A |Will not be Accessed|1|testNegLedgerEntryListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_LEDGERBOOK_710|Get Ledger Entry List at Division Level| N/A |Will not be Accessed|1|testNegLedgerEntryListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_LEDGERBOOK_720|Get Ledger Entry List at Mandal Level| N/A |Will not be Accessed|1|testNegLedgerEntryListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_LEDGERBOOK_770|Search Ledger Entry at State Level| N/A |Will not be Accessed|1|testNegSearchLedgerEntryAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_LEDGERBOOK_780|Search Ledger Entry at District Level| N/A |Will not be Accessed|1|testNegSearchLedgerEntryAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_LEDGERBOOK_790|Search Ledger Entry at Division Level| N/A |Will not be Accessed|1|testNegSearchLedgerEntryAtDivLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_LEDGERBOOK_970|Export Ledger Entry Pdf at State Level| N/A |Will not be exported|1|testNegExportLedgerEntryPdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_LEDGERBOOK_980|Export Ledger Entry List Pdf at State Level| N/A |Will not be exported|1|testNegExportLedgerEntryListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_LEDGERBOOK_990|Export Ledger Entry Xlx at State Level| N/A |Will not be exported|1|testNegExportLedgerEntryXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_LEDGERBOOK_1000|Export Ledger Entry List Xlx at State Level| N/A |Will not be exported|1|testNegExportLedgerEntryListXlxAtStateLevel|
|1.0|Download|ut_n_p_GSTS_WEB_LEDGERBOOK_1010|Download Ledger Entry attachment at State Level| N/A |Will not be downloaded|1|testNegDownloadLedgerEntryAttachmentAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_LEDGERBOOK_1070|Panchayat1112 user trying to access Panchayat1111 Ledger Entry which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111LedgerEntry|
|1.0|Remove|ut_n_r_GSTS_WEB_LEDGERBOOK_1080|Panchayat1112 user trying to remove Panchayat1111 Ledger Entry which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111LedgerEntry|

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Ledger Book should be provided in the User Manual.

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




 
