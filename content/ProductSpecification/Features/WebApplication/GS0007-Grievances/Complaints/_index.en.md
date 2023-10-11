---
title: Complaints
tags : ["Composing"]
---

## Introduction
Complaints are one of the features of this software product. Users will have access to complaints if they have permission, Otherwise will not access. By using Complaints, Users can create the complaint and it will be assigned to the respected officer and it's status also monitored and notified through SMS,Email, and Whatsapp. User can track the complaint status using Complaint code.

## Business Assumptions
1. Complaints feature should be planned at the design phase.
1. Complaints Feature is accessible in all levels i.e. State level, Division level, District level, Mandal level, and Panchayat level.
1. Aadhaar number is required to create the complaint.

## Requirements
### Functional Requirements
1. We can create, view, and track complaints at any level.
1. User can create complaint in any panchayat.

### Non-functional Requirements
1. Single user can create many complaints.
1. Complaints can be tracked using Complaint Code.

### Problem Statement
Complaints feature contains information about all complaints which are created by users and Track complaints feature is required to track the status of the complaint.

### Design 
1. Each complaint has Complaint type, Status, Priority, description, code and  Aadhaar number.
1. Each complaint has unique code(complaint code).
1. We can create, track, view and export the complaint.
1. Comments on Complaint, Status, Assignee changes should be made in Comment Section.
1. Complaints can be tracked using Track Complaints feature.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	
|Citizen|[gs0006-citizens]({{< ref "gs0006-citizens" >}})|Parent page|	
|User|[gs0004-users]({{< ref "gs0004-users" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_complaint_list|To view all the complaints. This listing page should bind to a permission|
|uc_complaint_create|To create the complaint. This create page should bind to a permission|
|uc_complaint_view|To view the complaint. This view page should bind to a permission|
|uc_complaint_track|To track the complaint. This track page should bind to a permission|
|uc_complaint_search|To search the complaint. This search page should bind to a permission|
|uc_complaint_export|To export the complaint in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|type|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "complaint_type", length = 256, nullable = false)|complaint_type varchar(256) NOT NULL|YES|NO|NO|YES|YES|YES||
|status|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "status", length = 16, nullable = false)|status varchar(16) NOT NULL|YES|NO|NO|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9/:#, _.-[]()@,minlen=6,maxlen=128|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|NO|NO|YES|NO|NO||
|code|YES|NA|0-9|@Column(name = "code", length = 32, nullable = false)|code varchar(32) NOT NULL|NO|NO|NO|YES|YES|YES||
|priority|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "priority", length = 16, nullable = false)|priority varchar(16) NOT NULL|YES|NO|NO|NO|YES|NO||
|notifySms|YES|NA|Boolean|@Column(name = "sms_notify", nullable = false)|sms_notify boolean NOT NULL|YES|NO|NO|NO|NO|NO||
|notifyEmail|YES|NA|Boolean|@Column(name = "email_notify", nullable = false)|email_notify boolean NOT NULL|YES|NO|NO|NO|NO|NO||
|notifyWhatsapp|YES|NA|Boolean|@Column(name = "whatsapp_notify", nullable = false)|whatsapp_notify boolean NOT NULL|NO|NO|NO|YES|NO|NO||
|citizen|YES|NA|0-9|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "caid", referencedColumnName = "aid")|caid varchar(12) NOT NULL|YES|NO|NO|YES|YES|YES||
|assignee|YES|NA|DropDown Values|@ManyToOne(fetch = FetchType.LAZY)	@JoinColumn(name = "assignee_id", nullable = false)|assignee_id VARCHAR(36) NOT NULL|NO|NO|NO|YES|NO|YES||
|workflow|YES|NA|NA|@Column(name = "workflow", length = 256, nullable = true)|workflow varchar(256) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|fileName|YES|NA|Attachment|@Column(name = "file_name", length = 64, nullable = true)|file_name varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||


#### ENUM CONSTANTS

##### Complaint Type

{{<mermaid align="left">}}
classDiagram
    class ComplaintType{
      BLOCKAGE_OF_DRAINAGE
      MOSQUITO_OF_MENACE
      STREET_DOG_MENACE
      STAGNANT_OF_WATER_ON_THE_ROAD
      REGARDING_BIRTH_CERTIFICATE
      REGARDING_DEATH_CERTIFICATE
      REGARDING_INCOME_CERTIFICATE
      REGARDING_CASTE_CERTIFICATE
	  REGARDING_GOVT_SCHEMES
	  PIG_MENACE
	  MIXING_OF_WASTE_WATER_IN_DRINKING_WATER
	  DUST_BIN_REMOVAL
	  PUBLIC_HEALTH
	  UNSANITARY_CONDITIONS_ON_THE_ROAD
	  COMPLAINTS_REGARDING_DUST_SMOKE
	  DAMAGE_AGAINST_PUBLIC_PROPERTY
	  NEW_STREET_LIGHT
	  NON_BURNING_OF_STREET_LIGHTS
	  COMPLAINT_REGARDING_TOILET
	  IMPROPER_MAINTENANCE_OF_TOILET
	  BURNING_OF_STREET_LIGHT_DURING_DAY_TIME
	  BROKEN_OF_WATER_TANK
	  SALES_OF_WATER
	  NO_WATER_SUPPLY
	  REQUEST_TO_LAY_NEW_DRAINAGE_LINE
	  REQUEST_TO_RELY_THE_ROAD
	  NO_SPEED_BREAKER
	  ROAD_DAMAGE
	  ENCROACHMENT_OF_SAND_IN_PUBLIC_ROAD
	  COMPLAINT_REGARDING_STREET_NAME_BOARD
	  ENCROACHMENT_OF_ROCKS_IN_PUBLIC_ROAD
	  WATER_TANK_REQUEST
	  REQUEST_TO_SWIMMING_POOL
	  DELAY_OF_PENSION
	  DELAY_IN_CHANGING_THE_NAME_IN_CERTIFICATE
	  TAX_COLLECTIONS
	  OTHERS
    }
{{< /mermaid >}}

##### Complaint Status Type

{{<mermaid align="left">}}
classDiagram
    class ComplaintStatusType{
      OPEN
      IN_PROGRESS
      CLOSED
      EXPIRED
      HOLD
      REJECTED
    }
{{< /mermaid >}}

##### Complaint Priority

{{<mermaid align="left">}}
classDiagram
    class ComplaintPriority{
      Low
      Medium
      High
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|COMPLAINT_VIEW|View|
|COMPLAINT_CREATE|Create|
|COMPLAINT_TRACK|Track|
|COMPLAINT_VIEW|Export|
|COMPLAINT_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Foreign Keys|1.fk__gs_complaint__caid FOREIGN KEY (caid) REFERENCES gs_citizen (aid)|
||2. fk__gs_complaint__assignee_id FOREIGN KEY (assignee_id) REFERENCES gs_user (id)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|AC_ROLE_COMPLAINT_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_COMPLAINT_TRACK|Only user having the user role with this permission should track the complaint using code|
|AC_ROLE_COMPLAINT_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_COMPLAINT_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Track page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
#### Complaints
{{<mermaid align="left">}}
flowchart TD
	ComplaintsMenu((Complaints Menu))
	ListPage{Complaints List Page}
	CreatePage((Create Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->ComplaintsMenu
    subgraph Menu
    ComplaintsMenu
    end
    subgraph   
    ComplaintsMenu-->ListPage
    ListPage--C-V-E-->ListPage
    end
    subgraph  
    ComplaintsMenu--F-->ErrorPage
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

#### Track Complaints
{{<mermaid align="left">}}
flowchart TD
	ComplaintsMenu((Track Complaints Menu))
	TrackPage((Track Page))
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->ComplaintsMenu
    subgraph Menu
    ComplaintsMenu
    end
    subgraph  
    ComplaintsMenu--F-->ErrorPage
    ErrorPage-->Stop   
    end
    subgraph Track
    ComplaintsMenu--T-->TrackPage
    TrackPage--S-->TrackPage
    end
    %%For success Representation
    linkStyle 3 stroke:green,stroke-width:2px;
    linkStyle 4 stroke:#cc33ff,stroke-width:2px;
    %%For failure representation
    linkStyle 1 stroke:red,stroke-width:2px;
    %%linkStyle 5 stroke:red,stroke-width:2px;

        
{{< /mermaid >}}


|Symbol|Action|
|:-----|:-----|
|C|Create|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|T|Track|
|SB|Submit or Back|
|C-V-E|Create or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|
|Pink Arrow|Success or Failure|

### Sequence Diagram
1. Only a user with the COMPLAINT_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant ComplaintListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/ctx/Complaint/list ListPage
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S:  GET /app/ctx/Complaint/list ListPage
        cloud-->>-ComplaintListPage: RES: List Page
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/create/form CreateFormPage
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : GET /app/Complaint/create/form CreateFormPage
        cloud-->>-ComplaintListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, POST /app/Complaint/create Create
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : POST /app/Complaint/create Create
        cloud-->>-ComplaintListPage: RES: An Complaint Successfully Created
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/view ViewPage
        Net--x-ComplaintListPage: F : Connection Error
        alt
		note right of Net:  Complaint Cache Object Found
        ComplaintListPage->>+Cache: S : GET /app/Complaint/view ViewPage
        Cache-->>-ComplaintListPage: RES: complaint View
        else
		note right of Net:  Complaint Cache Object Not Found
        Cache->>+cloud: GET /app/Complaint/view ViewPage
        cloud-->>-ComplaintListPage: RES: complaint View
        end
        ComplaintListPage->>+Net: Check Internet, POST /app/ComplaintComment/create ComplaintComment
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : POST /app/ComplaintComment/create ComplaintComment
        cloud-->>-ComplaintListPage: RES: An ComplaintComment Successfully Created 
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/track/form TrackFormPage
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : GET /app/Complaint/track/form TrackFormPage
        cloud-->>-ComplaintListPage: RES: Track Form Loaded
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, POST /app/Complaint/track Track
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : POST /app/Complaint/track Track
        cloud-->>-ComplaintListPage: RES: Complaint Object
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/exportPdf ExportPdf
        Net--x-ComplaintListPage: F : Connection Error
        alt
		note right of Net:  Complaint Cache Object Found
        ComplaintListPage->>+Cache: S : GET /app/Complaint/exportPdf ExportPdf
        Cache-->>-ComplaintListPage: RES: complaint Pdf
        else
		note right of Net:  Complaint Cache Object Not Found
        Cache->>+cloud: GET /app/Complaint/exportPdf ExportPdf
        cloud-->>-ComplaintListPage: RES: complaint Pdf
        end
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/exportListPdf ExportListPdf
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : GET /app/Complaint/exportListPdf ExportListPdf
        cloud-->>-ComplaintListPage: RES: complaint List Pdf
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/exportXlx ExportXlx
        Net--x-ComplaintListPage: F : Connection Error
        alt
		note right of Net:  Complaint Cache Object Found
        ComplaintListPage->>+Cache: S : GET /app/Complaint/exportXlx ExportXlx
        Cache-->>-ComplaintListPage: RES: Complaint Xlx
        else
		note right of Net:  Complaint Cache Object Not Found
        Cache->>+cloud: GET /app/Complaint/exportXlx ExportXlx
        cloud-->>-ComplaintListPage: RES: complaint Xlx
        end
    end
    rect rgb(244,244,244)
        ComplaintListPage->>+Net: Check Internet, GET /app/Complaint/exportListXlx ExportListXlx
        Net--x-ComplaintListPage: F : Connection Error
        ComplaintListPage->>+cloud: S : GET /app/Complaint/exportListXlx ExportListXlx
        cloud-->>-ComplaintListPage: RES: complaint List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_WEB_COMPLAINT_101 ut_n_c_GSTS_WEB_COMPLAINT_102 ut_n_c_GSTS_WEB_COMPLAINT_109 ut_n_c_GSTS_WEB_COMPLAINT_110 ut_n_c_GSTS_WEB_COMPLAINT_111 ut_n_c_GSTS_WEB_COMPLAINT_112|**Positive Test Cases:** Creating Complaint with Authorised User **Negative Test Cases:** 1.Creating Complaint with Invalid Inputs 2.Creating Complaint without DB Connection 3.Creating Complaint At Dist Level with Authorised user 4.Creating Complaint At Div Level with Authorised user 5.Creating Complaint At Mandal Level with Authorised user| **citizenAid:** 1.Valid characters 2.length=12 3.null **ComplaintType:** Enum values:37 **ComplaintPriority:** Enum values:3 **descr:** 1.Valid characters 2.length>6 and length<256 3.null **notifySms:** Boolean **notifyEmail:** Boolean **notifyWhatsapp:** Boolean|37|8|45|testAuthorisedUserCreateComplaint, testAuthorisedUserCreateComplaintNegativeTestCase, testAuthorisedUserCreateComplaintWithoutDBConnection, testAuthorisedUserCreateComplaintAtDistLevel, testAuthorisedUserCreateComplaintAtDivLevel, testAuthorisedUserCreateComplaintAtMandalLevel|
|1.0|Create Form|ut_p_c_GSTS_WEB_COMPLAINT_108|Open Complaint Create Form with Authorised user|N/A|1|0|1|testAuthorisedUserOpenComplaintCreateForm|
|1.0|Comment|ut_p_cc_GSTS_WEB_COMPLAINT_200 ut_n_cc_GSTS_WEB_COMPLAINT_201 ut_n_cc_GSTS_WEB_COMPLAINT_203 ut_n_cc_GSTS_WEB_COMPLAINT_204 ut_n_cc_GSTS_WEB_COMPLAINT_205|**Positive Test Cases:** Creating Complaint Comment with Authorised User **Negative Test Cases:** 1.Complaint Comment Create with Invalid Inputs 2.Complaint Comment Create with Complaint Status:Hold 3.Complaint Comment Create with Complaint Status: Closed 4.Complaint Comment Create with Complaint Status: Rejected| **assigneeName:** 1.Valid Assignee Id 2.Invalid Assignee Id **ComplaintStatusType:** Enum values:6 **descr:** 1.Valid characters 2.length>6 and length<256 3.null **ComplaintId:** 1.Valid Id 2.Invalid Id |1|4|5|testAuthorisedUserComplaintCommentCreate, testComplaintCommentCreateNegativeTestcase, testAuthorisedUserComplaintCommentCreateWithComplaintStatusHold, testComplaintCommentCreateWithComplaintStatusClosed, testComplaintCommentCreateWithComplaintStatusRejected|
|1.0| View |ut_p_v_GSTS_WEB_COMPLAINT_300 ut_p_v_GSTS_WEB_COMPLAINT_302 ut_p_v_GSTS_WEB_COMPLAINT_303 ut_p_v_GSTS_WEB_COMPLAINT_304 ut_n_v_GSTS_WEB_COMPLAINT_301 ut_n_v_GSTS_WEB_COMPLAINT_306 |**Positive Test Cases:** View Complaint with Valid Id  with Authorised User 2.View Complaint At Dist level with Authorised User 3.View Complaint At Division level with Authorised User 4.View Complaint At Mandal level with Authorised User **Negative Test Cases:** 1.View Complaint with Invalid ID with Authorised User|1.Valid Id 2.Invalid Id|4|2|6|testAuthorisedUserViewComplaint, testAuthorisedUserViewComplaintWithInvalidId, testAuthorisedUserViewComplaintAtDistLevel, testAuthorisedUserViewComplaintAtDivLevel, testAuthorisedUserViewComplaintAtMandalLevel, testAuthorisedUserViewComplaintWithoutDBConnection|
|1.0| Search |ut_p_s_GSTS_WEB_COMPLAINT_400 ut_n_s_GSTS_WEB_COMPLAINT_401 ut_n_s_GSTS_WEB_COMPLAINT_402 ut_n_s_GSTS_WEB_COMPLAINT_404|**Positive Test Cases:** Search Complaint with Authorised User **Negative Test Cases:** 1.Search Complaint with Invalid Inputs 2.Search Complaint without DB Connection 3.Search Complaint with Invalid dates with Authorised User| **citizenAid:** 1.Valid characters 2.length=12 **ComplaintType:** Enum values **status:** Enum values **code:** 1.Valid characters 2.length>3 and length<32|4|4|8|testAuthorisedUserSearchComplaint, testAuthorisedUserSearchComplaintNegativetestCases, testAuthorisedUserSearchComplaintWithoutDBConnection, testAuthorisedUserSearchComplaintNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_COMPLAINT_500 ut_p_l_GSTS_WEB_COMPLAINT_503 ut_p_l_GSTS_WEB_COMPLAINT_507 ut_p_l_GSTS_WEB_COMPLAINT_511 ut_p_l_GSTS_WEB_COMPLAINT_515 ut_n_l_GSTS_WEB_COMPLAINT_501 ut_n_l_GSTS_WEB_COMPLAINT_504 ut_n_l_GSTS_WEB_COMPLAINT_506 ut_n_l_GSTS_WEB_COMPLAINT_510 ut_n_l_GSTS_WEB_COMPLAINT_514 ut_n_l_GSTS_WEB_COMPLAINT_518 |**Positive Test Cases:** 1.Check the object list with valid data  with Authorised User 2.Check the Inprogress list with Authorised User 3.Check the Pending list with Authorised User 4.Check the Complaint Closed list with Authorised User 5.Check the Complaint Rejected list with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User 2.Check the Complaint Inprogress list with InValid data 3.Check the Complaint Penidng list without DB Connection|Validating with unique field 4.Check the Complaint Inprogress list without DB Connection 5.Check the Complaint Closed list without DB Connection 6.Check the Complaint Rejected list without DB Connection|5|6|11|testAuthorisedUserListComplaint, testAuthorisedUserListComplaintNegativeTestCase, testAuthorisedUserComplaintInprogressComplaint, testAuthorisedUserComplaintInprogressListNegativeTestCase, testAuthorisedUserComplaintInprogressListWithoutDBConnection, testAuthorisedUserComplaintPendingList, testAuthorisedUserComplaintPendingListWithoutDBConnection, testAuthorisedUserComplaintClosedList, testAuthorisedUserComplaintClosedListWithoutDBConnection, testAuthorisedUserComplaintRejectedList, testAuthorisedUserComplaintRejectedListWithoutDBConnection|
|1.0| Track |ut_p_s_GSTS_WEB_COMPLAINT_600 ut_n_s_GSTS_WEB_COMPLAINT_603 ut_n_s_GSTS_WEB_COMPLAINT_604|**Positive Test Cases:** Track Complaint with Authorised User **Negative Test Cases:** 1.Track Complaint without DB Connection 2.Track Complaint with Invalid code|  **code:** 1.valid characters 2.length>3 and length<32 3.null|1|2|3|testComplaintTrack, testComplaintTrackWithoutDBConnection, testComplaintTrackWithInvalidCode|
|1.0| Track Form |ut_p_s_GSTS_WEB_COMPLAINT_602|**Positive Test Cases:** Open Complaint Track Form with Authorised user|N/A|1|0|1|testAuthorisedUserOpenComplaintTrackForm|
|1.0| PDF |ut_p_ep_GSTS_WEB_COMPLAINT_800 ut_n_ep_GSTS_WEB_COMPLAINT_805 ut_n_ep_GSTS_WEB_COMPLAINT_812 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_COMPLAINT_801 ut_n_elp_GSTS_WEB_COMPLAINT_806 ut_n_elp_GSTS_WEB_COMPLAINT_813 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_COMPLAINT_802 ut_n_ex_GSTS_WEB_COMPLAINT_807 ut_n_ex_GSTS_WEB_COMPLAINT_814 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_COMPLAINT_803 ut_n_elx_GSTS_WEB_COMPLAINT_808 ut_n_elx_GSTS_WEB_COMPLAINT_815 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_n_c_GSTS_WEB_COMPLAINT_105|Unauthorised User does not have permission to create| **citizenAid:** 1.Valid characters 2.length=12 3.null **ComplaintType:** Enum values:37 **ComplaintPriority:** Enum values:3 **descr:** 1.Valid characters 2.length>6 and length<256 3.null **notifySms:** Boolean **notifyEmail:** Boolean **notifyWhatsapp:** Boolean|0|1|1|testUnAuthorisedUserCreateComplaint|
|1.0|Comment|ut_n_cc_GSTS_WEB_COMPLAINT_202 |Unauthorised User does not have permission to comment the complaint| **assigneeName:** 1.Valid Assignee Id 2.Invalid Assignee Id **ComplaintStatusType:** Enum values:6 **descr:** 1.Valid characters 2.length>6 and length<256 3.null **ComplaintId:** 1.Valid Id 2.Invalid Id |0|1|1|testUnAuthorisedUserComplaintCommentCreate|
|1.0| View |ut_n_v_GSTS_WEB_COMPLAINT_305 |Unauthorised User does not have permission to view the complaint|1.Valid Id 2.Invalid Id|0|1|1|testUnAuthorisedUserViewComplaint|
|1.0| Search |ut_n_s_GSTS_WEB_COMPLAINT_403 |**Positive Test Cases:** Search Complaint with Authorised User **Negative Test Cases:** Search Complaint with Authorised User| **citizenAid:** 1.Valid characters 2.length=12 **ComplaintType:** Enum values **status:** Enum values **code:** 1.Valid characters 2.length>3 and length<32|0|1|1|testUnAuthorisedUserSearchComplaint|
|1.0| List |ut_n_l_GSTS_WEB_COMPLAINT_502 ut_n_l_GSTS_WEB_COMPLAINT_505 ut_n_l_GSTS_WEB_COMPLAINT_509 ut_n_l_GSTS_WEB_COMPLAINT_513 ut_n_l_GSTS_WEB_COMPLAINT_517|Unauthorised User does not have permission to view the list of complaints|Validating with unique field|0|1|1|testUnAuthorisedUserListComplaint|testUnAuthorisedUserComplaintInprogressList, testUnAuthorisedUserListComplaint, testUnAuthorisedUserComplaintPendingList, testUnAuthorisedUserComplaintClosedList, testUnAuthorisedUserComplaintRejectedList|
|1.0| Track |ut_n_s_GSTS_WEB_COMPLAINT_601 |Unauthorised User does not have permission to Track the complaint|  **code:** 1.valid characters 2.length>3 and length<32 3.null |0|1|1|testUnAuthorisedUserTrackComplaint|
|1.0| PDF |ut_n_ep_GSTS_WEB_COMPLAINT_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_COMPLAINT_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_COMPLAINT_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_COMPLAINT_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------| 
|1.0|Create|ut_n_c_GSTS_WEB_COMPLAINT_700| Creating Complaint at state level with authorised User| N/A |Will be created|1|testAuthorisedUserCreateComplaintAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_COMPLAINT_701|View State Level Complaint At Panchayat Level Context with Authorised User| N/A |User not able to view the Complaint at state level|1|testAuthorisedUserSearchStateLevelComplaintAtPanchayatLevel|

## Security compliance check
1. Only user having the permission **ROLE_COMPLAINT_VIEW** should view this functionality 
1. Only user having the permission **ROLE_COMPLAINT_CREATE** should create this functionality 
1. Only user having the permission **ROLE_COMPLAINT_TRACK** should remove this functionality 
1. Only user having the permission **ROLE_COMPLAINT_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Complaints should be provided in the User Manual.

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




 
