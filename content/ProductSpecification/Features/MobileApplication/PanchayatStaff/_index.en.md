---
title: GS0003 - Panchayat Staff
tags : ["Composing"]
---

## Introduction
Panchayat staff is one of the basic features of the software product, which is used to store  the details  of Panchayat Staff members like president,secretary,ward member,contract employee e.t.c.

## Business Assumptions  
1. Panchayat staff feature should be planned at the design phase.  
1. Panchyat staff Creation Should be takes place,after the Panchayat selection.  
1. Survey User need to select the panchyat for the creation of panchayat staff.  
## Requirements
### Functional Requirements
1. Before using the panchayat staff  feature, user should ***sign-in*** in the application.
1. In this feature, survey user should be create only one Panchyat President and Panchyat Secretary.
1. Survey User could be create  any number of staff members except president and secretary.
   
### Non-functional Requirements
1. In  this feature we don't allow, to create duplicate president and secretary.It may avoid data  inconsistency.
1. This Feature supports the 1000 of records per one survey User(Mobile device).1000 of records are easily load and gives better performance.   
1. Survey user can create panchyat staff, after the **Sign-in** and panchyat selection.It may includes the security.So this feature is only accessible for the survey user.
1. Multiple users can use  this feature to create panchyat staff  without internet.
1. Internet is required only when the survey user want to upload the data.

### Problem Statement
The Panchyat staff  feature is required to create panchayat staff members like president,secretary,ward member,contract employee e.t.c.
### Design
1. Panchyat staff feature has three pages.Those pages are  
   1. panchyat staff list page.  
   1. panchyat staff form page.  
   1. panchyat staff view page.  
1. Panchyat staff list page contains the list items to show the panchyat staff members data.It has search,delete,touch(view) functionalities.
1. Panchyat staff form page is a form page,which is designed according to the requirements to take the data of panchyat members like(name,aadhaar number,designation e.t.c).It has next button to navigate view page.
1. Panchyat staff view page is used to display the form data.View Page has edit button,to navigate view  to form page.It has edit functionality to edit the data.

#### Dependant Features
| Feature name        | Reference Link                                          | Remarks                                                                                           |
|---------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| Sign In             | [Login]({{< ref "Login" >}})                            | You can only use the panchayat Staff feature when you first ***sign-in***  in to the application. |
| Side Menu           | [Side Menu]({{< ref "Side Menu" >}})                    | Parent Page                                                                                       |
| Panchayat Selection | [Panchayat Selection]({{< ref "PanchayatSelection" >}}) | After selection of panchayat only survey user can create the panchyat staff.                      |
#### Use cases
#### Use cases
| Use case Code            | Description                  |
|--------------------------|------------------------------|
| uc_panchyat_staff_create | To create the panchyat staff |
| uc_panchyat_staff_view   | To view the panchyat staff   |
| uc_panchyat_staff_update | To update the panchyat staff |
| uc_panchyat_staff_search | To search the panchyat staff |
| uc_panchyat_staff_delete | To delete the panchyat staff |

#### Model Attributes
| Attribute name        | Mandatory | Default value | Input Allowed Char set Layout/API       | KV Database Key              | SQLite Column Definition     | Create | Update | Remove | View | List | Search | Remarks |
|-----------------------|-----------|---------------|-----------------------------------------|------------------------------|------------------------------|--------|--------|--------|------|------|--------|---------|
| id                    | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA                           | id String                    | YES    | YES    | YES    | NO   | NO   | NO     ||
| staffAid              | YES       | NA            | 0-9, maxlen=12                          | STAFF_AADHAAR_NUMBER_KEY     | staffAid String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffAadhaarInputType | YES       | OCR           | NA                                      | STAFF_AADHAAR_INPUT_TYPE     | staffAadhaarInputType String | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffName             | YES       | NA            | a-z A-Z, maxlen=64                      | STAFF_NAME_KEY               | staffName String             | YES    | YES    | YES    | YES  | YES  | YES    ||
| staffSurname          | YES       | NA            | a-z A-Z, maxlen=32                      | STAFF_SUR_NAME_KEY           | staffSurname String          | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffFsname           | YES       | NA            | a-zA-Z /, maxlen=64                     | STAFF_FATHER_SPOUSE_NAME_KEY | staffFsname String           | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffMobileNumber     | YES       | NA            | 0-9, maxlen=10                          | STAFF_MOBILE_KEY             | staffMobileNumber String     | YES    | YES    | YES    | YES  | YES  | YES    ||
| staffGender           | YES       | Male          | Radio Button Values                     | STAFF_GENDER_KEY             | staffGender String           | YES    | YES    | YES    | YES  | YES  | YES    ||
| staffDob              | YES       | NA            | 0-9/-, maxlen=10                        | STAFF_DOB_KEY                | staffDob String              | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffEmail            | NO        | NA            | 0-9, maxlen=3                           | STAFF_EMAIL_KEY              | staffEmail String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffDesg             | YES       | Choose        | a-zA-Z0-9.@$_#,:;()/\, maxlen=64        | STAFF_DESIGNATION_KEY        | staffDesg String             | YES    | YES    | YES    | YES  | YES  | YES    ||
| staffQualification    | YES       | Choose        | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | STAFF_QUALIFICATION          | staffQualification String    | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffJoinYear         | YES       | NA            | Date Picker                             | STAFF_JOINING_KEY            | staffJoinYear String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| staffImage            | YES       | None          | a-zA-Z0-9, maxlen=128                   | STAFF_IMAGE                  | staffImage String            | YES    | YES    | YES    | YES  | YES  | NO     ||
| dataSync              | YES       | NA            | 0(No), 1(Yes)                           | NA                           | dataSync Boolean             | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync             | YES       | NA            | 0(No), 1(Yes)                           | NA                           | imageSync Boolean            | NA     | NA     | NA     | NO   | NO   | NO     ||
| survey_pending        | YES       | Yes           | 0(No), 1(Yes)                           | SURVEY_PENDING_KEY           | survey_pending Boolean       | NA     | YES    | NA     | NO   | YES  | NO     ||
| survey_start_time     | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_START_TIME            | survey_start_time String     | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time       | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_END_TIME              | survey_end_time String       | YES    | NA     | NA     | YES  | NO   | NO     ||
| avgSurveyTime         | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_TIME                  | avgSurveyTime String         | YES    | NA     | NA     | YES  | NO   | NO     ||
| networkProviders      | NO        | NA            | a-zA-Z0-9, maxlen=128                   | NA                           | networkProviders String      | YES    | NA     | NA     | NO   | NO   | NO     ||
| response_error_msg    | YES       | NA            | a-zA-Z0-9, maxlen=NA                    | NA                           | responseErrorMsg String      | NO     | NA     | NA     | YES  | NO   | NO     ||
| is_encrypted          | YES       | NA            | 0(No) , 1(Yes)                          | NA                           | is_encrypted Boolean         | NA     | NA     | NA     | NO   | NO   | NO     ||


#### ENUM CONSTANTS

##### Aadhaar Input Type

{{<mermaid align="left">}}
classDiagram
class AadhaarInputType{
OCR
QRCODE
MANUAL
}
{{< /mermaid >}}

##### StaffDesignation

{{<mermaid align="left">}}
classDiagram
class StaffDesignation{
CHOOSE
PANCHAYAT_PRESIDENT
PANCHAYAT_SECRETARY
PANCHAYAT_WARD_MEMBER
CONTRACT_EMPLOYEE
}
{{< /mermaid >}}


##### EduQualificationType

{{<mermaid align="left">}}
classDiagram
class EduQualificationType{
CHOOSE
NONE
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
OTHER

}
{{< /mermaid >}}


#### Constraints
| Constraint  | Key |
|-------------|-----|
| Primary Key | id  |


#### Feature Permission
No feature permission for this  feature.

| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |
## Acceptance Criteria
| Description                                                                                  |
|----------------------------------------------------------------------------------------------|
| Version : 1.0                                                                                |
| 1. Survey User can able to Create, View, Update, Search, Delete and Sync the Panchyat Staff. |
| 1. Edit functionality doesn't works,after updation of the data to the server.                |

## User Experience
### Listing Page
{{<mermaid align="left">}}
graph LR
Add[+ Add Item]-->View[View Item]-->Search[Search Item]-->Delete[Delete Item]-->BackButton[<- Back]   
{{< /mermaid >}}

### Form Page
{{<mermaid align="left">}}
graph LR
Next[NEXT]-->BackButton[<- Back]
{{< /mermaid >}}

### View Page
{{<mermaid align="left">}}
graph LR
Finish[FINISH]-->BackButton[<- Back]
{{< /mermaid >}}

### List to View Page
{{<mermaid align="left">}}
graph LR
Edit[EDIT]-->BackButton[<- Back]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
SurveyItemsPage[Start / Continue Survey Page]
ListPage((Panchyat staff  List Page))
FromPage[Panchyat staff Form Page]
ConfirmationPage[Panchyat staff Details Confirmation Page]
PanchyatStaffItem[Panchyat staff Item]
ViewPage[PanchyatStaff View Page]
Start((Start))
AddBtn[Add Item Button]
NextBtn1[Next Button]
FinishBtn1[Finish Button]
EditBtn[Edit Button]
BackBtn1[Back Button]
PanchyatStaff[Panchyat staff ]
PanchyatStaffDelteItem[Panchyat staff Item]
DeletePanchyatStaffMessage>Panchyat staff Deleted]
End((end))
ErrorPage>Exception Message]
Start-->SurveyItemsPage
subgraph Taxable Properties
SurveyItemsPage--C-->PanchyatStaff
end
subgraph Error
PanchyatStaff--F-->ErrorPage
ErrorPage-->End
end
subgraph List Page
PanchyatStaff--S-->ListPage
ListPage--C-->AddBtn
ListPage--C-->PanchyatStaffItem
ListPage--SAD-->PanchyatStaffDelteItem
PanchyatStaffDelteItem--F-->ListPage
end
subgraph Form Page
AddBtn--S-->FromPage
AddBtn--F-->ListPage
FromPage--C-->NextBtn1
end
subgraph Details View Page
NextBtn1--F-->FromPage
NextBtn1--S-->ConfirmationPage
ConfirmationPage--C-->FinishBtn1
FinishBtn1--F-->ConfirmationPage
FinishBtn1--S-->ListPage
ConfirmationPage--C-->BackBtn1
BackBtn1--S-->FromPage
BackBtn1--F-->ConfirmationPage
end
subgraph View Page
PanchyatStaffItem--S-->ViewPage
PanchyatStaffItem--F-->ListPage
ViewPage--C-->EditBtn
EditBtn--F-->ViewPage
EditBtn--S-->FromPage
end
subgraph delete
PanchyatStaffDelteItem--S-->DeletePanchyatStaffMessage
end
%%For click Repressentation
linkStyle 1 stroke:blue,stroke-width:2px;
linkStyle 5 stroke:blue,stroke-width:2px;
linkStyle 6 stroke:blue,stroke-width:2px;
linkStyle 11 stroke:blue,stroke-width:2px;
linkStyle 14 stroke:blue,stroke-width:2px;
linkStyle 17 stroke:blue,stroke-width:2px;
linkStyle 22 stroke:blue,stroke-width:2px;
%%For success Representation
linkStyle 4 stroke:green,stroke-width:2px;
linkStyle 9 stroke:green,stroke-width:2px;
linkStyle 13 stroke:green,stroke-width:2px;
linkStyle 16 stroke:green,stroke-width:2px;
linkStyle 18 stroke:green,stroke-width:2px;
linkStyle 20 stroke:green,stroke-width:2px;
linkStyle 24 stroke:green,stroke-width:2px;
linkStyle 25 stroke:green,stroke-width:2px;
%%For failure Representation
linkStyle 2 stroke:red,stroke-width:2px;
linkStyle 8 stroke:red,stroke-width:2px;
linkStyle 10 stroke:red,stroke-width:2px;
linkStyle 12 stroke:red,stroke-width:2px;
linkStyle 15 stroke:red,stroke-width:2px;
linkStyle 19 stroke:red,stroke-width:2px;
linkStyle 21 stroke:red,stroke-width:2px;
linkStyle 23 stroke:red,stroke-width:2px;
%%For delete Representation
linkStyle 7 stroke:orange,stroke-width:2px;

{{< /mermaid >}}

| Symbol      | Action          |
|:------------|:----------------|
| C           | ClickOn         |
| S           | OnSuccess       |
| F           | OnFailure       |
| SAD         | Swap And Delete |
| Blue Link   | Click           |
| Green Link  | Success         |
| Red Link    | Failure         |
| Orange Link | Delete          |


### Panchayat Staff flow : offline and online
### Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
Start((start))
End((end))
SurveyDashboard[Start / Continue Survey Page]
ListPage[Panchyat Staff Listing Page]
subgraph List Page
DBCallLoadAllPanchyatStaffs[load All Panchyat Staffs From SQLite DB]
SetPanchyatStaffsDatainListPage[Set Panchyat Staff Data in List Page]
end
subgraph Add Item
FormPage[Panchyat Staff Form Page]
end
subgraph Form Page
FormPageInitialSetUp[Panchyat Staff From Page Initial SetUp]
saveDatainKVDatabase[save Form Data in KvDataBase]
DataValidationCehck{Data Validation}
DetailsConfirmationPage[Panchyat Staff Details Confirmation Page]
ShowMessageDataValidation>Show Message: Please Enter Valid Data]
end
subgraph Details Confirmation Page
getDataFromKVDatabase[get Panchayat staff KV Data From KV Database]
setDataInConfirmationPage[set Panchyat Staff Data in Confirmation Page]
PreparePanchyatStaffObject[ Panchyat Staff Object Preparation]
DBCallInsertOrUpdatePanchyatStaffData[Insert / Update Panchyat Staff Object in SQLite DB]
end       
subgraph View Page
FetchPanchyatStaffByID[fetch PanchyatStaffById From SQLite DB]
setDataInViewPage[set Panchyat Staff Data in Veiw Page]
end    
Start-->SurveyDashboard
SurveyDashboard--Click Panchyat Staff-->ListPage
%%List page
ListPage-->DBCallLoadAllPanchyatStaffs
DBCallLoadAllPanchyatStaffs-->SetPanchyatStaffsDatainListPage
%%Add PanchyatStaff
ListPage--Add PanchyatStaff-->FormPage
FormPage-->FormPageInitialSetUp
FormPageInitialSetUp--Input PanchyatStaff Data-->saveDatainKVDatabase
saveDatainKVDatabase-->DataValidationCehck
DataValidationCehck--Valid-->DetailsConfirmationPage
DataValidationCehck--Not Valid-->ShowMessageDataValidation
%%Details Confirmation Page
DetailsConfirmationPage-->getDataFromKVDatabase
getDataFromKVDatabase-->setDataInConfirmationPage
setDataInConfirmationPage-->PreparePanchyatStaffObject
PreparePanchyatStaffObject-->DBCallInsertOrUpdatePanchyatStaffData
DBCallInsertOrUpdatePanchyatStaffData-->DBCallLoadAllPanchyatStaffs
%%Edit PanchyatStaff
ListPage--View PanchyatStaff-->FetchPanchyatStaffByID
FetchPanchyatStaffByID-->setDataInViewPage
setDataInViewPage--Edit-->FormPage
ListPage-->End
{{< /mermaid >}}

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
participant SQLite as SQLite Database
participant ListPage as Panchyat Staff Listing Page
participant FormPage as Panchyat Staff Form Page
participant KVDB as KV Database
participant ViewPage as Panchyat Staff View Page
autonumber

    rect rgb(244,244,244)
        ListPage->>+SQLite: load All Panchyat Staff details
        SQLite-->>-ListPage: List Of Panchyat Staff details
    end
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new Panchyat Staff ) (3) else { (7) } 
        FormPage->>+KVDB: save Panchyat Staff KV Data in KVDatabase
    end
    
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get Panchyat Staff KV Data 
        KVDB-->>-ViewPage: KV Panchyat Staff Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update update Panchyat Staff} else {insert Panchyat Staff}
        ViewPage->>+SQLite: updatePanchyatStaff(Panchyat Staff) (or) insertPanchyatStaff(Panchyat Staff) 
    end  
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end
    rect rgb(244,244,244)
        Note left of ViewPage: View Panchyat Staff Data
        ViewPage->>+SQLite: fetchPanchyatStaffById(id) 
        SQLite-->>-ViewPage: Panchyat Staff Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit Panchyat Staff Data
        FormPage->>+SQLite: fetchPanchyatStaffById(id) 
        SQLite-->>-FormPage: Panchyat Staff Object
    end    
    rect rgb(244,244,244)
        Note right of FormPage: Repeat (3) to (6)
    end
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (1) and (2)
    end    

{{< /mermaid >}}


## Security compliance check
1. Only login user can able to view the Panchayat Staff Feature.
## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Panchayat Staff in the User Manual. It's scope is limited to Developer Technical Document

## Feature/Defect list
| Feature/Defect ID | Link                                                     | Status |
|-------------------|----------------------------------------------------------|--------|
| GS-0002           | [GS-0002](https://shadkona.atlassian.net/browse/GS-0002) | Closed |


## References
1. [Android Developer Docs](https://developer.android.com/docs)

## Development Estimations
| Release Tag | Feature/Defect ID | Scrum Details   | Start date  | End date    |
|-------------|-------------------|-----------------|-------------|-------------|
| 2020OCT     | GS-0002           | Scrum 2020OCTs2 | 14 OCT 2020 | 28 OCT 2020 |

## Feature Doneness Criteria
Check list for the Doneness criteria

| Metric                       | Unit Measure | Expected Result | Actual Result | Accepted? | Remarks               | Approver  |
|------------------------------|--------------|-----------------|---------------|-----------|-----------------------|-----------|
| Acceptance Criteria Defined? | YES or NO    | YES             | YES           | Accepted  | All test cases passed | PM        |
| Architecture Approved?       | YES or NO    | YES             | YES           | Accepted  | Design is accepted    | Architect |
| Coding Completed?            | YES or NO    | YES             | YES           | Completed | Completed             | EM        |
| Product Defects              | Number       | 0               | 0             | Accepted  || EM                    |
| Unit Test Case Count?        | Number       | >5              | 8             | Accepted  | Tested                | EM        |
| Integration Test Cases Count | Number       | >5              | 9             | Accepted  | Tested                | EM        |
| Sonar Vulnerabilities Count  | Number       | 0               | 0             | Accepted  | validated             | EM        |
| Code Coverage                | Number       | >98%            | 99%           | Accepted  | Validated             | EM        |
| User Manual Verified?        | YES or NO    | YES             | YES           | Accepted  | Validated             | DocM      |
| PenTest Defect Count?        | Number       | <2              | 0             | Accepted  | Validated             | EM        |
| PM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | PM        |
| OM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |
| Deployed to Staging?         | YES or NO    | YES             | YES           | Accepted  | Good to go            | EM        |
| Deployed to Production?      | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |













