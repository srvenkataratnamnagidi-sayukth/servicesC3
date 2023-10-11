---
title: Families
tags : ["Composing"]
---

## Introduction
Families are one of the features of our software product. The product holds the information of families from various panchayat's. User should have the permission to access this feature.

## Business Assumptions
Updating and removing the families can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
Each and every citizen living in the panchayat are created and mapped to their family. Every family
should contain one family head and a set of citizens.

### Non-functional Requirements
System can support any number of families but this design will limit 15,00,000 families for this system. Beyond the 15,00,000 families  may experience performance issues. 

### Problem Statement
Families holds the information of a house and set of citizens belongs to a house in a panchayat.

### Design 
1. We can Create, Update, View, and remove the families.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_family_create|To create the family|
|uc_family_update|To update the family|
|uc_family_remove|To remove the family|
|uc_family_view|To view the family|
|uc_family_search|To search the family|
|uc_family_export|To export the family in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Drinking Water Type|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "drink_water", length = 16, nullable = false)|drink_water varchar(16) not null|YES|YES|YES|YES|YES|YES||
|Primary Crop|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "primary_crop", length = 6, nullable = false)|primary_crop varchar(6) not null|YES|YES|YES|YES|YES|YES||
|Farm Water Type|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "farm_water", length = 10, nullable = false)|farm_water varchar(10) not null|YES|YES|YES|YES|NO|NO||
|Ration Card Type|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "ration_type", length = 6, nullable = false)|ration_type varchar(6) not null|YES|YES|YES|YES|YES|YES||
|Family Head Aadhaar Number|YES|NA|Allowed 0-9 and length should be 12|@Column(name = "aid", length = 12, nullable = false)|aid varchar(12) not null |YES|NO|YES|YES|YES|YES||
|Number of Citizens without Aadhaar|YES|NA|Allowed 0-9, >=0|@Column(name = "no_aadhaar_count", nullable = false)|no_aadhaar_count bigint(20) NOT NULL|YES|YES|YES|YES|NO|NO||
|Family Members Aadhaar Number|NO|NA|Allowed 0-9 and length should be 12|@JsonIgnore @ManyToMany(fetch = FetchType.LAZY) @JoinTable(name = "gs_family_citizen_map", joinColumns = { @JoinColumn(name = "fid", nullable = false) }, inverseJoinColumns = { @JoinColumn(name = "cid", nullable = false, referencedColumnName = "aid") }, uniqueConstraints = @UniqueConstraint (columnNames = { "fid", "cid" }))| uk_gs_family_citizen_map__cid__fid (cid,fid) CONSTRAINT fk__gs_family_citizen_map__fid FOREIGN KEY (fid) REFERENCES gs_family (id) |YES|YES|NO|YES|NO|NO||
|House Property Name|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 64|@ManyToOne @JoinColumn(name = "house_property_id", nullable = false)|house_property_id varchar(36) not null|YES|YES|NO|YES|NO|NO||
|Updated Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|Removed Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### Enum Constants

##### Drinking Water Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      NONE
      OWN_WELL
      HAND_WELL
      MOTOR_WELL
      POND
      PUBLIC_WELL
      PUBLIC_TAP
      PRIVATE_TAP
      OTHER
      SELF_WATER_PURIFIER
    }
{{< /mermaid >}}

##### Primary Crop

{{<mermaid align="left">}}
classDiagram
    class Name{
      NONE 
      RICE 
      WHEAT 
      AQUA
      MILLET
      PULSES
      OTHER
    }
{{< /mermaid >}}

##### Farm Water Type

{{<mermaid align="left">}}
classDiagram
    class Name{
    NONE 
    RAIN 
    CANAL 
    MOTOR_BORE 
    POND 
    OTHER
    }
{{< /mermaid >}}

##### Ration Card Type

{{<mermaid align="left">}}
classDiagram
    class Name{
    NONE
    WHITE
    PINK
    GREEN
    AAY
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|FAMILY_CREATE|Create|
|FAMILY_UPDATE|Update|
|FAMILY_REMOVE|Remove|
|FAMILY_VIEW|View|
|FAMILY_VIEW|List|
|FAMILY_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|uk__gs_family__aid (aid)|
||uk_gs_family_citizen_map__cid__fid (cid,fid)|
|Foreign Keys|fk__gs_family_citizen_map__fid FOREIGN KEY (fid) REFERENCES gs_family (id)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_family_create|Only user having the permission to create, should create this functionality|
|ac_family_update|Only user having the permission to update, should update this functionality|
|ac_family_remove|Only user having the permission to remove, should remove this functionality|
|ac_family_view|Only user having the permission to view, should view this functionality|
|ac_family_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

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
	FamiliesMenu((Families Menu))
	ListPage{Families List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->FamiliesMenu
    subgraph Menu
    FamiliesMenu
	end
	subgraph List
	FamiliesMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	FamiliesMenu-->ErrorPage
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

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
||||
||||

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant FamiliesListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet, GET /app/ctx/Family/list ListPage
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S:  GET /app/ctx/Family/list ListPage
        cloud-->>-FamiliesListPage: RES:List Page
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet, GET /app/Family/create/form CreateFormPage
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : GET /app/Family/create/form CreateFormPage
        cloud-->>-FamiliesListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: POST /app/Family/create Create
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : POST /app/Family/create Create
        cloud-->>-FamiliesListPage: RES: An Family Successfully Created
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/update/form UpdateFormPage
        Net--x-FamiliesListPage: F : Connection Error
        alt
        Note right of Net: Family Cache Object Found
        FamiliesListPage->>+Cache: S : GET /app/Family/update/form UpdateFormPage
        Cache-->>-FamiliesListPage: RES: Update Form Loaded
        else
        Note right of Net: Family Cache Object Not Found
        Cache->>+cloud: GET /app/Family/update/form UpdateFormPage
        cloud-->>-FamiliesListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: POST /app/Family/update update
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : POST /app/Family/update Update
        cloud-->>-FamiliesListPage: RES: An Family Successfully Updated
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/remove/form RemoveFormPage
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : GET /app/Family/remove/form RemoveFormPage
        cloud-->>-FamiliesListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: POST /app/Family/remove Remove
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : POST /app/Family/remove Remove
        cloud-->>-FamiliesListPage: RES: A Family Successfully Removed
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/view ViewPage
        Net--x-FamiliesListPage: F : Connection Error
        alt
        Note right of Net: Family Cache Object Found
        FamiliesListPage->>+Cache: S : GET /app/Family/view ViewPage
        Cache-->>-FamiliesListPage: RES: family View
        else
        Note right of Net: Family Cache Object Not Found
        Cache->>+cloud: GET /app/Family/view ViewPage
        cloud-->>-FamiliesListPage: RES: family View
        end
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/exportPdf ExportPdf
        Net--x-FamiliesListPage: F : Connection Error
        alt
        Note right of Net: Family Cache Object Found
        FamiliesListPage->>+Cache: S : GET /app/Family/exportPdf ExportPdf
        Cache-->>-FamiliesListPage: RES: family Pdf
        else
        Note right of Net: Family Cache Object Not Found
        Cache->>+cloud: GET /app/Family/exportPdf ExportPdf
        cloud-->>-FamiliesListPage: RES: family Pdf
        end
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/exportListPdf ExportListPdf
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : GET /app/Family/exportListPdf ExportListPdf
        cloud-->>-FamiliesListPage: RES: family List Pdf
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/exportXlx ExportXlx
        Net--x-FamiliesListPage: F : Connection Error
        alt
        Note right of Net: Family Cache Object Found
        FamiliesListPage->>+Cache: S : GET /app/Family/exportXlx ExportXlx
        Cache-->>-FamiliesListPage: RES: family Xlx
        else
        Note right of Net: Family Cache Object Not Found
        Cache->>+cloud: GET /app/Family/exportXlx ExportXlx
        cloud-->>-FamiliesListPage: RES: family Xlx
        end
    end
    rect rgb(244,244,244)
        FamiliesListPage->>+Net: Check Internet: GET /app/Family/exportListXlx ExportListXlx
        Net--x-FamiliesListPage: F : Connection Error
        FamiliesListPage->>+cloud: S : GET /app/Family/exportListXlx ExportListXlx
        cloud-->>-FamiliesListPage: RES: family List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_p_c_GSTS_WEB_FAMILY_100 ut_n_c_GSTS_WEB_FAMILY_101 ut_p_c_GSTS_WEB_FAMILY_108 ut_n_c_GSTS_WEB_FAMILY_109 ut_n_c_GSTS_WEB_FAMILY_110 ut_p_c_GSTS_WEB_FAMILY_111 ut_n_c_GSTS_WEB_FAMILY_112 ut_n_c_GSTS_WEB_FAMILY_113 ut_n_c_GSTS_WEB_FAMILY_114 ut_n_c_GSTS_WEB_FAMILY_115 ut_n_c_GSTS_WEB_FAMILY_116|**Positive Test Cases:** Creating Family with Authorised User **Negative Test Cases:** 1.Creating Family with Invalid Inputs 2.Creating Family without DB Connection| **headAid:** 1.Valid characters 2.length=12 3.null **drinkWaterType:** Enum values:10 **primaryCrop:** Enum values:7 **farmWaterType:** Enum values:6 **rationCardType:** Enum values:5|10|3|13| testAuthorisedUserCreateFamily, testAuthorisedUserCreateFamilyNegativeTestCase, testAuthorisedUserCreateFamilyUptoWizardStep2, testAuthorisedUserCreateFamilyUptoWizardStep2WithEmptyCitizenId, testAuthorisedUserCreateFamilyUptoWizardStep3WithInvalidFamilyCitizen, testAuthorisedUserCreateFamilyUptoWizardStep3, testAuthorisedUserCreateFamilyUptoWizardStep3WithInvalidInput, testAuthorisedUserCreateFamilyUptoWizardStep2WithInvalidCitizen, testAuthorisedUserCreateFamilyUptoWizardStep3WithInvalidCitizen, testCreateFamilyUptoWizardStep3WithInvalidFamilyCitizen, testAuthorisedUserCreateFamilyWithoutDBConnection|
|1.0| Create Form |ut_p_c_GSTS_WEB_FAMILY_107 ut_n_v_GSTS_WEB_FAMILY_11 |**Positive Test Cases:** Open Family Create Form with Authorised User **Negative Test Cases:** Open Family Create Form without DB Connection |N/A|1|0|1|testAuthorisedUserOpenFamilyCreateForm|
|1.0|Update| ut_p_u_GSTS_WEB_FAMILY_204 ut_p_u_GSTS_WEB_FAMILY_213 ut_n_u_GSTS_WEB_FAMILY_203 ut_n_u_GSTS_WEB_FAMILY_205 ut_p_u_GSTS_WEB_FAMILY_207 ut_p_u_GSTS_WEB_FAMILY_208 ut_n_u_GSTS_WEB_FAMILY_209 ut_n_u_GSTS_WEB_FAMILY_210 ut_n_u_GSTS_WEB_FAMILY_211 ut_n_u_GSTS_WEB_FAMILY_212 ut_n_u_GSTS_WEB_FAMILY_214 ut_n_u_GSTS_WEB_FAMILY_215 ut_n_u_GSTS_WEB_FAMILY_216 |**Positive Test Cases:** Updating Family with Authorised User **Negative Test Cases:** 1.Updating Family with Invalid Inputs 2.Updating Family without DB Connection 3.Updating Family upto wizard step 2 with new citizen aid 4.Updating Family with Invalid RelationWithHeadType 5.Updating Family with Invalid Inputs 6.Updating Family with Invalid RelationWithHeadType| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |2|3|5|testAuthorisedUserUpdateFamilyWithoutDBConnection, testAuthorisedUserUpdateFamily, testAuthorisedUserUpdateFamilyNegativeTestCase, testAuthorisedUserUpdateFamilyUptoWizardStep2, testAuthorisedUserUpdateFamilyUptoWizardStep3, testAuthorisedUserUpdateFamilyWithInvalidFamilyHeadAid, testAuthorisedUserUpdateFamilyWithDifferentFamilyHeadAid, testAuthorisedUserUpdateFamilyWithInvalidFamilyMemberRelation, testAuthorisedUserUpdateFamilyUptoWizardStep2WithNewCitizenAid, testAuthorisedUserUpdateFamilyPosTc, testAuthorisedUserUpdateFamilyWithInvalidRelationWithHeadType, testAuthorisedUserUpdateFamilyWithInvalidInputs, testAuthorisedUserUpdateFamilyWithInvalidCitizenRelationWithHeadType|
|1.0| Update Form |ut_n_u_GSTS_WEB_FAMILY_200 ut_n_u_GSTS_WEB_FAMILY_201 |**Positive Test Cases:** Open Family Update Form with Authorised User **Negative Test Cases:** 1.Open Family Create Form without DB Connection 2. Open Family Update form with Invalid Id |N/A|1|1|2|testAuthorisedUserOpenFamilyUpdateFormWithInvalidId, testAuthorisedUserOpenFamilyUpdateFormWithoutDBConnection|
|1.0|Remove| ut_p_r_GSTS_WEB_FAMILY_306 ut_n_r_GSTS_WEB_FAMILY_303 ut_n_r_GSTS_WEB_FAMILY_304 ut_n_r_GSTS_WEB_FAMILY_305 ut_n_r_GSTS_WEB_FAMILY_307  |**Positive Test Cases:** Removing Family with Authorised User **Negative Test Cases:** 1.Removing Family with Invalid Inputs 2.Removing Family without DB Connection| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|1|2|testAuthorisedUserRemoveFamilyWithInvalidCommentAndId, testAuthorisedUserRemoveFamilyWithInvalidId, testAuthorisedUserRemoveFamilyWithoutDBConnection, testAuthorisedUserRemoveFamily, testAuthorisedUserRemoveFamilyNegativeTestCase|
|1.0| Remove Form |ut_p_r_GSTS_WEB_FAMILY_300 ut_n_r_GSTS_WEB_FAMILY_301 ut_n_r_GSTS_WEB_FAMILY_201 |**Positive Test Cases:** Open Family Remove Form with Authorised User **Negative Test Cases:** 1.Open Remove Create Form without DB Connection 2. Open Remove Update form with Invalid Id |N/A|1|1|2|testAuthorisedUserOpenFamilyRemoveForm, testAuthorisedUserOpenFamilyRemoveFormWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_FAMILY_400 ut_n_v_GSTS_WEB_FAMILY_401 |**Positive Test Cases:** View Family with Valid Id  with Authorised User**Negative Test Cases:** 1.View Family with Invalid ID |1.Valid Id 2.Invalid Id|1|1|2|testAuthorisedUserViewFamilyWithValidId, testAuthorisedUserViewFamilyWithInValidId|
|1.0| Search |ut_p_s_GSTS_WEB_FAMILY_500 ut_n_s_GSTS_WEB_FAMILY_501 ut_n_s_GSTS_WEB_FAMILY_503 ut_n_s_GSTS_WEB_FAMILY_504 |**Positive Test Cases:** Search Family with Authorised User **Negative Test Cases:** 1.Search Family with Invalid Inputs 2.Search Family without DB Connection| **aid:** 1.valid characters 2.length=4 or length=12 **drinkWaterType:** Enum values **primaryCrop:** Enum values **rationCardType:** Enum values|5|2|7|testAuthorisedUserSearchFamily, testAuthorisedUserSearchFamilyNegativeTestCase, testAuthorisedUserSearchFamilyWithoutDBConnection, testAuthorisedUserSearchFamilyNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_FAMILY_600 ut_n_l_GSTS_WEB_FAMILY_601 ut_n_l_GSTS_WEB_FAMILY_603 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data 2.Check the object list without DB Connection|Validating with unique field|1|1|2|testAuthorisedUserListFamily, testAuthorisedUserListFamilyNegativeTestCase, testAuthorisedUserListFamilyWithoutDBConnection| 
|1.0| PDF |ut_p_ep_GSTS_WEB_FAMILY_800 ut_n_ep_GSTS_WEB_FAMILY_804 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_FAMILY_801 ut_n_elp_GSTS_WEB_FAMILY_805 ut_n_elp_GSTS_WEB_FAMILY_812 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_FAMILY_802 ut_n_ex_GSTS_WEB_FAMILY_806 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_FAMILY_803 ut_n_elx_GSTS_WEB_FAMILY_807 ut_n_elx_GSTS_WEB_FAMILY_813 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|---| 
|1.0| Create | ut_n_c_GSTS_WEB_FAMILY_104|Unauthorised User does not have permission to create| **headAid:** 1.Valid characters 2.length=12 3.null **drinkWaterType:** Enum values:10 **primaryCrop:** Enum values:7 **farmWaterType:** Enum values:6 **rationCardType:** Enum values:5|1|N/A|1| testUnAuthorisedUserCreateFamily|
|1.0|Update| ut_n_u_GSTS_WEB_FAMILY_202|Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|N/A|1|testUnAuthorisedUserUpdateFamily|
|1.0| Update Form |ut_n_u_GSTS_WEB_FAMILY_206|Unauthorised User does not have permission to open update form|1.Valid Id|1|N/A|1|testUnAuthorisedUserOpenFamilyUpdateForm|
|1.0|Remove| ut_n_r_GSTS_WEB_FAMILY_308|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|N/A|1|testUnAuthorisedUserRemoveFamily|
|1.0| Remove Form |ut_n_r_GSTS_WEB_FAMILY_302|Unauthorised User does not have permission to open remove form|1.Valid Id|1|N/A|1|testUnAuthorisedUserOpenFamilyRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_FAMILY_402|Unauthorised User does not have permission to view|1.Valid Id|1|N/A|1|testUnAuthorisedUserViewFamilyWithValidId|
|1.0| Search |ut_n_s_GSTS_WEB_FAMILY_502|Unauthorised User does not have permission to search| **aid:** 1.valid characters 2.length=4 or length=12 **drinkWaterType:** Enum values **primaryCrop:** Enum values **rationCardType:** Enum values|1|N/A|1|testUnAuthorisedUserSearchFamily|
|1.0| List |ut_n_l_GSTS_WEB_FAMILY_602|Unauthorised User does not have permission to list|Validating with unique field|1|N/A|1|testUnAuthorisedUserListFamily|
|1.0| PDF |ut_n_ep_GSTS_WEB_FAMILY_808 |Export List Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_FAMILY_809 |Export Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_FAMILY_810 |Export XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_FAMILY_811 |Export List XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|----------| 
|1.0|Create|ut_n_c_GSTS_WEB_FAMILY_700| Creating Family at state level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateFamilyAtStateLevl| 
|1.0|View|ut_n_v_GSTS_WEB_FAMILY_701| View Family at state level with authorised user| N/A |User not able to view the Family at state level|1|testAuthorisedUserViewFamilyAtStateLevel| 
|1.0|View|ut_n_v_GSTS_WEB_FAMILY_403| View Family at Different Panchayat with authorised user| N/A |User not able to view the Family at Different Panchayat|1|testAuthorisedUserViewFamilyWithValidIdAtDifferentPanchayat| 
|1.0|Search|ut_n_s_GSTS_WEB_FAMILY_505| Search Family at state level with authorised user| N/A |User not able to search the Family at state level|1|testAuthorisedUserSearchFamilyAtStateLevel|
## Security compliance check
1. Only user having the user role with permission **ROLE_FAMILY_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_FAMILY_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_FAMILY_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_FAMILY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the FAMILIES in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
