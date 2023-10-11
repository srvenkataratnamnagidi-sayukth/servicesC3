---
title: GS0018 - Govt Schemes
tags : ["Composing"]
---

## Introduction
Government Schemes is one of the feature of this software product. Government Schemes are Schemes which are released by government to make something official. Users will have access to government schemes if they have permission, Otherwise will not access. 

## Business Assumptions
what type of users can create government schemes should be planned at design phase.

## Requirements
### Functional Requirements
1. Any level of user can view government schemes if they have permission.
1. we can create government schemes at the state level only.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access govt orders.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Government Schemes contain information about all government schemes which are released by government.

### Design 
1. Each govt scheme has name, description, code(government scheme number), govt order copy,Ration card Type,Living Type,Caste Category,Education Status,Education School,Education Qualification,Income category,Gender, Marital Status,Disability Type,Disable min age, Disabled Max age, General Insurance,Health Insurance,Self helping groups,bank account,Occupation and Employment status.
1. Each govt scheme has unique code.
1. We can create, view and export the government schemes.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_government_scheme_create|To create the government scheme. This create page should bind to a permission|
|uc_government_scheme_list|To view all the government schemes. This listing page should bind to a permission|
|uc_government_scheme_view|To view the government scheme. This view page should bind to a permission|
|uc_government_scheme_search|To search the government scheme. This search page should bind to a permission|
|uc_government_scheme_export|To export the government scheme in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9. space _-, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|YES|NO|NO||
|code|YES|NA|a-zA-Z0-9, minlen=3, maxlen=32|@Column(name = "code", length = 32, nullable = false, unique = true)|code varchar(32) NOT NULL|YES|NO|YES|NO||
|fileName|YES|NA|Attachment|@Column(name = "file_name", length = 64, nullable = false)|file_name varchar(64) NOT NULL|YES|YES|YES|NO||
|rationCardSet|YES|NA|Enum Values|@ElementCollection(targetClass = RationCardType.class) @CollectionTable(name = "gs_scheme_ration", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|livingTypeSet|YES|NA|Enum Values|@ElementCollection(targetClass = LivingPlaceType.class) @CollectionTable(name = "gs_scheme_living_place", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|castCatSet|YES|NA|Enum Values|@ElementCollection(targetClass = CasteCategoryType.class) @CollectionTable(name = "gs_scheme_cast_cat", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|eduStatusSet|YES|NA|Enum Values|@ElementCollection(targetClass = EduStatusType.class) @CollectionTable(name = "gs_scheme_edu_status", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|eduSchoolTypeSet|YES|NA|Enum Values|@ElementCollection(targetClass = EduSchoolType.class) @CollectionTable(name = "gs_scheme_edu_school", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|eduQualificationSet|YES|NA|Enum Values|@ElementCollection(targetClass = EduQualificationType.class) @CollectionTable(name = "gs_scheme_edu_qualification", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|incomeSet|YES|NA|Enum Values|@ElementCollection(targetClass = IncomeCategoryType.class) @CollectionTable(name = "gs_scheme_income_cat", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|genderSet|YES|NA|Enum Values|@ElementCollection(targetClass = GenderType.class) @CollectionTable(name = "gs_scheme_gender", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|martialStatusSet|YES|NA|Enum Values|@ElementCollection(targetClass = MaritalStatusType.class) @CollectionTable(name = "gs_scheme_married", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|disabledStatusSet|YES|NA|Enum Values|@ElementCollection(targetClass = DisabledStatusType.class) @CollectionTable(name = "gs_scheme_disabled", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|occupationSet|YES|NA|Enum Values|@ElementCollection(targetClass = EmpOccupationType.class) @CollectionTable(name = "gs_scheme_occupation", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|empStatusSet|YES|NA|Enum Values|@ElementCollection(targetClass = EmpStatusType.class) @CollectionTable(name = "gs_scheme_income_emp_status", joinColumns = @JoinColumn(name = "sid"))@Enumerated(EnumType.STRING)@Column(name = "evalue")|evalue varchar(32) NOT NULL|YES|NO|NO|NO||
|minAge|YES|NA|0-9 maxlen=64|@Column(name = "min_age", nullable = true)|min_age bigint(20) DEFAULT NULL|YES|NO|NO|NO||
|maxAge|YES|NA|0-9 maxlen=64|@Column(name = "max_age", nullable = true)|max_age bigint(20) DEFAULT NULL|YES|NO|NO|NO||
|genInsurrance|YES|NA|Boolean|@Column(name = "ins_gen", nullable = true)|ins_gen boolean DEFAULT false|YES|NO|NO|NO||
|healthInsurrance|YES|NA|Boolean|@Column(name = "ins_health", nullable = true)|ins_health boolean DEFAULT false|YES|NO|NO|NO||
|womenGrp|YES|NA|Boolean|@Column(name = "women_grp", nullable = true)|women_grp boolean DEFAULT false|YES|NO|NO|NO||
|bankAcc|YES|NA|Boolean|@Column(name = "bank_acc", nullable = true)|bank_acc boolean DEFAULT false|YES|NO|NO|NO||


#### ENUM CONSTANTS
##### Gender

{{<mermaid align="left">}}
classDiagram
    class Name{
      MALE
      FEMALE
      OTHER
    }
{{< /mermaid >}}

##### Marital Status

{{<mermaid align="left">}}
classDiagram
    class Name{
      SINGLE
      MARRIED 
      DIVORCED 
      WIDOWED
      SEPERATED
      SPOUSE_DEAD
      LIVING_RELATION
    }
{{< /mermaid >}}

##### Caste Category

{{<mermaid align="left">}}
classDiagram
    class Name{
      OC
      BC
      SC
      ST
      MINORITY
      OTHERS
      NONE
    }
{{< /mermaid >}}

##### Education Status

{{<mermaid align="left">}}
classDiagram
    class Name{
      STUDYING 
      COMPLETED 
      DISCONTINUED 
      ILLITERATE 
      NONE
    }
{{< /mermaid >}}

##### Education Qualification 

{{<mermaid align="left">}}
classDiagram
    class Name{
      NURSERY 
      PRIMARY 
      SECONDARY 
      SSC 
      ITI 
      INTERMEDIATE 
      DIPLOMA 
      GRADUATE 
      POST_GRADUATE 
      DOCTORATE
      NONE 
      OTHER 
    }
{{< /mermaid >}} 
   
##### Occupation

{{<mermaid align="left">}}
classDiagram
    class Name{
      SMALL_FARMER 
      LEASE_FARMER 
      FARMER 
      FARMER_LABOUR 
      DAILY_LABOUR 
      FARMER_ANIMAL_HUSBANDRY 
      BUSINESS 
      EMPLOYEE_PVT
      EMPLOYEE_CONTRACT 
      EMPLOYEE_GOVT 
      EMPLOYEE_PART_TIME 
      NONE
    }
{{< /mermaid >}} 

##### Disability Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      BLIND
      DEAF
      DUMB
      LEGS
      HANDS
      MENTAL
      NONE 
      OTHER 
    }
{{< /mermaid >}} 

##### Long Disease Type

{{<mermaid align="left">}}
classDiagram
    class Name{
	  DIABETES
	  BP
	  CARDIAC
	  BP_DIABETES
	  CARDIAC_DIABETES
	  BP_CARDIAC
	  BP_CARDIAC_DIABETES
	  OTHER
	  NONE    
    }
{{< /mermaid >}} 

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|GOVT_SCHEME_CREATE|Create|
|GOVT_SCHEME_VIEW|Export|
|GOVT_SCHEME_VIEW|List|
|GOVT_SCHEME_VIEW|View|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_scheme__name (name)|
|Unique Key|uk__gs_scheme__code (code)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_GOVT_SCHEME_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_GOVT_SCHEME_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_GOVT_SCHEME_VIEW|Only user having the user role with this permission should list this functionality|
|AC_ROLE_GOVT_SCHEME_VIEW|Only user having the user role with this permission should export the government scheme in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	GovtSchemesMenu((Govt Scheme Menu))
	ListPage{Govt Schemes List Page}
	CreatePage((Create Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->GovtSchemesMenu
    subgraph Menu
    GovtSchemesMenu
    end
	subgraph   
    GovtSchemesMenu-->ListPage
    ListPage--C-V-E-->ListPage
    end
    subgraph  
    GovtSchemesMenu--F-->ErrorPage
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
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
        
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
|C-V-E|Create or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the GOVT_SCHEME_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant GovtSchemesListpage as Browser
    participant Net as Browser Net Tools
   	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet, GET /app/ctx/GovtScheme/list ListPage
        Net--x-GovtSchemesListpage: F : Connection Error
        GovtSchemesListpage->>+cloud: S:  GET /app/ctx/GovtScheme/list ListPage
        cloud-->>-GovtSchemesListpage: RES:List Page
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet, GET /app/GovtScheme/create/form CreateFormPage
        Net--x-GovtSchemesListpage: F : Connection Error
        GovtSchemesListpage->>+cloud: S : GET /app/GovtScheme/create/form CreateFormPage
        cloud-->>-GovtSchemesListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: POST /app/GovtScheme/create Create
        Net--x-GovtSchemesListpage: F : Connection Error
        GovtSchemesListpage->>+cloud: S : POST /app/GovtScheme/create Create
        cloud-->>-GovtSchemesListpage: RES: An Govt Scheme Successfully Created
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: GET /app/GovtScheme/view ViewPage
        Net--x-GovtSchemesListpage: F : Connection Error
        alt
        Note right of Net: Govt Scheme Cache Object Found
        GovtSchemesListpage->>+Cache: S : GET /app/GovtScheme/view ViewPage
        Cache-->>-GovtSchemesListpage: RES: Govt Scheme View
        else
        Note right of Net: Govt Scheme Cache Object Not Found
        Cache->>+cloud: GET /app/GovtScheme/view ViewPage
        cloud-->>-GovtSchemesListpage: RES: Govt Scheme View
        end
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: GET /app/GovtScheme/exportPdf ExportPdf
        Net--x-GovtSchemesListpage: F : Connection Error
        alt
        Note right of Net: Govt Scheme Cache Object Found
        GovtSchemesListpage->>+Cache: S : GET /app/GovtScheme/exportPdf ExportPdf
        Cache-->>-GovtSchemesListpage: RES: Govt Scheme Pdf
        else
        Note right of Net: Govt Scheme Cache Object Not Found
        Cache->>+cloud: GET /app/GovtScheme/exportPdf ExportPdf
        cloud-->>-GovtSchemesListpage: RES: Govt Scheme Pdf
        end
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: GET /app/GovtScheme/exportListPdf ExportListPdf
        Net--x-GovtSchemesListpage: F : Connection Error
        GovtSchemesListpage->>+cloud: S : GET /app/GovtScheme/exportListPdf ExportListPdf
        cloud-->>-GovtSchemesListpage: RES: Govt Scheme List Pdf
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: GET /app/GovtScheme/exportXlx ExportXlx
        Net--x-GovtSchemesListpage: F : Connection Error
        alt
        Note right of Net: Govt Scheme Cache Object Found
        GovtSchemesListpage->>+Cache: S : GET /app/GovtScheme/exportXlx ExportXlx
        Cache-->>-GovtSchemesListpage: RES: Govt Scheme Xlx
        else
        Note right of Net: Govt Scheme Cache Object Not Found
        Cache->>+cloud: GET /app/GovtScheme/exportXlx ExportXlx
        cloud-->>-GovtSchemesListpage: RES: Govt Scheme Xlx
        end
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: GET /app/GovtScheme/exportListXlx ExportListXlx
        Net--x-GovtSchemesListpage: F : Connection Error
        GovtSchemesListpage->>+cloud: S : GET /app/GovtScheme/exportListXlx ExportListXlx
        cloud-->>-GovtSchemesListpage: RES: Govt Scheme List Xlx
    end
    rect rgb(244,244,244)
        GovtSchemesListpage->>+Net: Check Internet: GET /app/GovtScheme/download DownloadCopy
        Net--x-GovtSchemesListpage: F : Connection Error
        GovtSchemesListpage->>+cloud: S : GET /app/GovtScheme/download DownloadCopy
        cloud-->>-GovtSchemesListpage: RES: Govt Scheme Copy
    end
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----| 
|1.0| Create |ut_p_c_GSTS_WEB_GOVTSCHEME_102 ut_p_c_GSTS_WEB_GOVTSCHEME_105 ut_n_c_GSTS_WEB_GOVTSCHEME_103 ut_n_c_GSTS_WEB_GOVTSCHEME_106 |**Positive Test Cases:** 1.Creating Govt Scheme with Authorised User 2.Creating GovtScheme with Authorised user at panchayat context **Negative Test Cases:** 1.Creating Govt Scheme with Invalid Inputs 2.Creating GovtScheme without DB Connection|**name:** <br>  1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null **code:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null 4.unique key  **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null **GenderType** **MaritalStatusType** **DisabledStatusType** **RationCardType** **LivingPlaceType** **CasteCategoryType** **EduStatusType** **EduSchoolType** **EduQualificationType** **IncomeCategoryType** **EmpOccupationType** **EmpStatusType**|12|6|18|testCreateGovtScheme, testCreateGovtSchemeNegativeCases, testCreateGovtSchemeAtPanchayatContext, testAuthorisedUserCreateGovtSchemeWithoutDBConnection|
|1.0| Create Form|ut_p_c_GSTS_WEB_GOVTSCHEME_100 ut_p_c_GSTS_WEB_GOVTSCHEME_101|**Positive Test Cases:** 1.Open GovtScheme Create form At State level with Authorised user 2.Open GovtScheme Create form At Panchayat level with Authorised user|N/A|2|0|2|testOpenGovtSchemeCreateForm, testOpenGovtSchemeCreateFormAtPanchayatLvl|
|1.0|Update|N/A| N/A | N/A |N/A|N/A|N/A||
|1.0|Remove|N/A| N/A | N/A |N/A|N/A|N/A||
|1.0| Delete |N/A|N/A| N/A |N/A|N/A|N/A||
|1.0| View |ut_p_v_GSTS_WEB_GOVTSCHEME_300 ut_n_v_GSTS_WEB_GOVTSCHEME_301 ut_n_v_GSTS_WEB_GOVTSCHEME_303 |**Positive Test Cases:** View Govt Scheme with Valid Id  with Authorised User**Negative Test Cases:** 1.View Govt Scheme with Invalid ID with Authorised User 2.View Govt Scheme with valid Id without DB Connection|1.Valid Id 2.Invalid ID|1|2|3|testAuthorisedUserViewGovtSchemeValidId, testAuthorisedUserViewGovtSchemeInValidId, testAuthorisedUserViewGovtSchemeValidIdWithoutDBConnection|
|1.0| Search |ut_p_s_GSTS_WEB_GOVTSCHEME_400 ut_p_s_GSTS_WEB_GOVTSCHEME_404 ut_n_s_GSTS_WEB_GOVTSCHEME_401 ut_n_s_GSTS_WEB_GOVTSCHEME_403 ut_n_s_GSTS_WEB_GOVTSCHEME_404 |**Positive Test Cases:** Search Govt Scheme with Authorised User **Negative Test Cases:** 1.Search Govt Scheme with Invalid Inputs 2.Search Govt Scheme without DB Connection 3.Search Govt Scheme with Invalid dates with Authorised User|**name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null |11|5|16|testAuthorisedUserSearchGovtScheme, testAuthorisedUserSearchGovtSchemeNegativeCase, testAuthorisedUserSearchGovtSchemeWithoutDBConnection, testSearchGovtScheme, testAuthorisedUserSearchGsNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_GOVTSCHEME_200 ut_p_l_GSTS_WEB_GOVTSCHEME_203  ut_n_l_GSTS_WEB_GOVTSCHEME_201 ut_n_l_GSTS_WEB_GOVTSCHEME_204|**Positive Test Cases:** 1.Check the object list with valid data  with Authorised User 2.Check the object list with valid data with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field 2.Check the object list with valid data Without DB Connection|2|2|4|testAuthorisedUserListGovtScheme, testAuthorisedUserListGovtSchemeNegativeCase, testAuthorisedUserListGovtSchemeAtPanchayatContext, testAuthorisedUserListGovtSchemeWithoutDBConnection|
|1.0| Download|ut_p_d_GSTS_WEB_GOVTSCHEME_500 ut_n_d_GSTS_WEB_GOVTSCHEME_501 ut_n_d_GSTS_WEB_GOVTSCHEME_503|**Positive Test Cases:** 1.Download Govt Scheme Attachment with Authorised User **Negative Test Cases:** 1.Download Govt Scheme Attachment with Invalid Id 2.Download Govt Scheme Attachment without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserDownloadGovtSchemeAttachment, testAuthorisedUserDownloadGovtSchemeAttachmentWithInvalidId, testAuthorisedUserDownloadGovtSchemeAttachmentWithoutDBConnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_GOVTSCHEME_800 ut_n_ep_GSTS_WEB_GOVTSCHEME_805 ut_n_ep_GSTS_WEB_GOVTSCHEME_812 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_GOVTSCHEME_801 ut_n_elp_GSTS_WEB_GOVTSCHEME_806 ut_n_elp_GSTS_WEB_GOVTSCHEME_813 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_GOVTSCHEME_802 ut_n_ex_GSTS_WEB_GOVTSCHEME_807 ut_n_ex_GSTS_WEB_GOVTSCHEME_814 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_GOVTSCHEME_803 ut_n_elx_GSTS_WEB_GOVTSCHEME_808 ut_n_elx_GSTS_WEB_GOVTSCHEME_815 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_n_c_GSTS_WEB_GOVTSCHEME_104|Unauthorised User does not have permission to create|  **name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null **code:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null 4.unique key  **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null|0|1|1|testUnAuthorisedUserCreateGovtScheme|
|1.0|Update|N/A| N/A | N/A |N/A|N/A|N/A|
|1.0|Remove|N/A| N/A | N/A |N/A|N/A|N/A|
|1.0| Delete |N/A| N/A | N/A |N/A|N/A|N/A|
|1.0| View |ut_n_v_GSTS_WEB_GOVTSCHEME_302|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnAuthorisedUserViewGovtOrder|
|1.0| Search |ut_n_s_GSTS_WEB_GOVTSCHEME_402|Unauthorised User does not have permission to search|  **name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null|0|1|1|testUnAuthorisedUserSearchGovtOrder|
|1.0| List |ut_n_l_GSTS_WEB_GOVTSCHEME_202|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testUnAuthorisedUserListGovtScheme|
|1.0| Download|ut_n_d_GSTS_WEB_GOVTSCHEME_502|Download Govt Scheme Attachment with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserDownloadGovtSchemeAttachment|
|1.0| PDF |ut_n_ep_GSTS_WEB_GOVTSCHEME_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_GOVTSCHEME_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_GOVTSCHEME_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_GOVTSCHEME_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|----|
|1.0|Create|ut_n_c_GSTS_WEB_GOVTSCHEME_12| Creating Govtscheme at panchayat level| N/A |Will not be Created|1|testCreateGovtSchemeAtPanchayatContext|

## Security compliance check
1. Only user having the permission **ROLE_GOVT_SCHEME_VIEW** should view this functionality 
1. Only user having the permission **ROLE_GOVT_SCHEME_CREATE** should create this functionality 
1. Only user having the permission **ROLE_GOVT_SCHEME_VIEW** should export this functionality
1. Only user having the permission **ROLE_GOVT_SCHEME_VIEW** should List this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Government Orders in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
