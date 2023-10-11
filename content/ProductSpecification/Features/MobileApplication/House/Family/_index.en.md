---
title: Family
tags : ["Composing"]
---

## Introduction
Family is one of the basic features of the software product which contains the data of all the
 families in the Telangana state. By using this family feature we have to store every
 family data.The product holds the information of families from various panchayats. Every Family should 
 be stored under respective panchayat only. 
## Business Assumptions
1. Family feature should be planned at the design phase.
1. User should be in the panchayat level to create the Family.
1. Creation of Family is depends on Creation of house.
1. The family is allowed to create only after the house has been created.
1. Survey User can able to sync the Family along with house to GS-Cloud. i.e Family data is also synced when house data is synced.


## Requirements
### Functional Requirements
1. Family feature only accessible in panchayat level.
1. Family Creation is two types which is based on ***Own house***  condition.Two types of family creations are 
    1. Owner Family
        1. If any family lives in their own house, we will Consider that family under the Owner Family.
    1. Other Family
        1. If any family does not lives in their own house, we will Consider that family under the Other Family.
1. If Own house is **yes** then we have to allow to create two types of families.Otherwise we have to allow Other Family only.
1. If Own house is **yes** then we must and should be create the Owner Family. Otherwise we may or may not to create the families.  
1. Each and every citizen living in the panchayat are created and mapped to their family. 
1. Every family should contain one family head and a set of citizens.


### Non-functional Requirements
1. System can support any number of families but this design will limit 15,00,000 families for this system. Beyond the 15,00,000.
### Problem Statement
Families holds the information of a house and set of citizens belongs to a house in a panchayat.
### Design 
1. We can Create, Update, View the Families.
2. Deletion of family must be done  at the time of deletion of house only.
3. Updation of family is unable when we sync that family data to Gs-cloud.

#### Checks on the Family module

1. Based on the Agricultural Farm we show or hide the field Agricultural Farm Water Type If Agricultural Farm is None  then we will hide the Agricultural Farm Water Type  field
2. Based on the Owner & Head Same check we will show/hide the Add Owner Label If Owner & Head Same is Yes then we hide the Add Owner Label else we will show it
#### Dependant Features
| Feature name | Reference Link | Remarks    |
|--------------|----------------|------------|
| Citizen      | -              | Child Page |
#### Use cases
| Use case Code    | Description          |
|------------------|----------------------|
| uc_family_create | To create the Family |
| uc_family_view   | To view the Family   |
| uc_family_update | To update the Family |

#### Model Attributes
| Attribute name               | Mandatory | Default value | Input Allowed Char set Layout/API | KV Database Key    | SQLite Column Definition | Create | Update | Remove | View | List | Search | Remarks                               |
|------------------------------|-----------|---------------|-----------------------------------|--------------------|--------------------------|--------|--------|--------|------|------|--------|---------------------------------------|
| id                           | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                 | id String                | YES    | YES    | YES    | NO   | NO   | NO     ||
| houseId                      | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                 | houseId String           | YES    | YES    | YES    | NO   | NO   | NO     ||
| aid                          | YES       | NA            | 0-9,maxlen=12                     | HEAD_AADHAR_KEY    | aid String               | YES    | NO     | YES    | NO   | NO   | No     ||
| name                         | YES       | NA            | a-z A-Z, maxlen=64                | HEAD_NAME_KEY      | name String              | YES    | NO     | YES    | NO   | YES  | NO     ||
| surname                      | YES       | NA            | a-z A-Z, maxlen=32                | NA                 | surname String           | YES    | NO     | YES    | NO   | NO   | NO     ||
| fsname                       | YES       | NA            | a-z A-Z, maxlen=64                | NA                 | fsname String            | YES    | NO     | YES    | NO   | NO   | NO     ||
| gender                       | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                 | gender String            | YES    | NO     | YES    | NO   | YES  | NO     ||
| agricultural_farm_type       | YES       | Choose        | DropDown Values                   | PRIMARY_CROP       | primaryCrop String       | YES    | YES    | YES    | NO   | YES  | NO     ||
| agricultural_farm_water_type | YES       | Choose        | DropDown Values                   | FARM_WATER_KEY     | farmWaterType String     | YES    | YES    | YES    | NO   | YES  | NO     ||
| drinking_water               | YES       | Choose        | DropDown Values                   | DRINKING_WATER_KEY | drinkingWater String     | YES    | YES    | YES    | NO   | YES  | NO     ||
| ration_Card_type             | YES       | Choose        | DropDown Values                   | RATION_CARD        | rationCardType String    | YES    | YES    | YES    | NO   | YES  | NO     ||
| no_aadhaar_count             | YES       | 0             | DropDown Values                   | NO_AADHAAR_COUNT   | noAadhaarCount String    | YES    | YES    | YES    | NO   | YES  | NO     |
| house_scheme_type            | YES       | Choose        | Spinner Values                    | HOUSE_SCHEME_TYPE  | houseSchemeType String   | YES    | YES    | YES    | YES  | NO   | NO     | Newly added field (30th January 2023) |
| job_card                     | YES       | False         | a-zA-Z, maxlen=NA                 | JOB_CARD           | jobCard Boolean          | YES    | YES    | YES    | YES  | NO   | NO     ||
| dataSync                     | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                 | dataSync Boolean         | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync                    | YES       | NA            | a-zA-Z0-9, maxlen=128             | NA                 | imageSync Boolean        | NA     | NA     | NA     | NO   | NO   | NO     ||


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

##### House Scheme Type
{{<mermaid align="left">}}
classDiagram
class Name{
NONE
NOT_APPLICABLE
SANCTIONED_CONSTRUCTION_NOT_STARTED
SANCTIONED_CONSTRUCTION_STOPPED
SANCTIONED_HAVING
SANCTIONED_UNDER_CONSTRUCTION
}
{{< /mermaid >}}



#### Feature Permission

| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |

#### Constraints
| Constraint  | Key |
|-------------|-----|
| Primary Key | id  |
## User Experience
### Create House Property
{{<mermaid align="left">}}
graph LR
    Add[+ Add Owner Family]--- AddFamily[+Add Family]--- BackButton[<- Back]   
{{< /mermaid >}}
### Family Form Page
{{<mermaid align="left">}}
graph LR
   AddHead[+AddHead]--- AddOwner[+Add Owner]--- AddPerson[+Add Person]--- Finish[Finish]--- BackButton[<- Back]
    
{{< /mermaid >}}
### View Page
{{<mermaid align="left">}}
graph LR
    Edit[Edit]--- Finish[Finish]---BackButton[<- Back]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	CreateHouseProperty((Create  House  Property   Create  House  Property))
	FormPage((Family Form Page Family Form Page Family Form Page))
    FamilyItem[Family Item]
    ViewPage[Family View Page]
	Start((Start))
    AddOwnerFamilyBtn[Add Owner Family +]
    AddFamilyBtn[Add Family +]
    FinishBtn[Finish Button]
    EditBtn[Edit Button]
    BackBtn[Back Button]
    AddHeadBtn[Add Head +]
    AddOwnerBtn[Add Owner +]
    AddPersonBtn[Add Person +]
    ReferToCitizen[Refer to citizen]
    Start-->CreateHouseProperty
    subgraph Create House Property
        CreateHouseProperty--C-->AddOwnerFamilyBtn
        linkStyle 1 stroke:blue,stroke-width:2px;
        CreateHouseProperty--C-->AddFamilyBtn
        linkStyle 2 stroke:blue,stroke-width:2px;
        CreateHouseProperty--C--> FamilyItem
        linkStyle 3 stroke:blue,stroke-width:2px;
    end   
    subgraph Family Form Page
        AddOwnerFamilyBtn--S-->FormPage
        linkStyle 4 stroke:green,stroke-width:2px;
        AddFamilyBtn--S-->FormPage
        linkStyle 5 stroke:green,stroke-width:2px;
        AddOwnerFamilyBtn--F-->CreateHouseProperty
        linkStyle 6 stroke:red,stroke-width:2px;
        AddFamilyBtn--F-->CreateHouseProperty
        linkStyle 7 stroke:red,stroke-width:2px;
    end
    subgraph Refer To Citizen
        FormPage--C-->AddHeadBtn--S-->ReferToCitizen
        linkStyle 8 stroke:blue,stroke-width:2px;
        linkStyle 9 stroke:green,stroke-width:2px;
        FormPage--C-->AddOwnerBtn--S-->ReferToCitizen
        linkStyle 10 stroke:blue,stroke-width:2px;
        linkStyle 11 stroke:green,stroke-width:2px;
        FormPage--C-->AddPersonBtn--S-->ReferToCitizen 
        linkStyle 12 stroke:blue,stroke-width:2px;
        linkStyle 13 stroke:green,stroke-width:2px;
        AddHeadBtn--F-->FormPage
        linkStyle 14 stroke:red,stroke-width:2px;
        AddOwnerBtn--F-->FormPage
        linkStyle 15 stroke:red,stroke-width:2px;
        AddPersonBtn--F-->FormPage
        linkStyle 16 stroke:red,stroke-width:2px;
    end    
    subgraph Back Button
       FormPage--C-->BackBtn--S-->CreateHouseProperty
       linkStyle 17 stroke:blue,stroke-width:2px;
       linkStyle 18 stroke:green,stroke-width:2px;
       BackBtn--F-->FormPage
       linkStyle 19 stroke:red,stroke-width:2px;
    end
    subgraph Family View Page
        FamilyItem--S-->ViewPage
        linkStyle 20 stroke:green,stroke-width:2px;
        FamilyItem--F-->CreateHouseProperty
        linkStyle 21 stroke:red,stroke-width:2px;
    end  
    subgraph Finish Button
        FormPage--C-->FinishBtn--S-->CreateHouseProperty
        linkStyle 22 stroke:blue,stroke-width:2px;
        linkStyle 23 stroke:green,stroke-width:2px;
        FinishBtn--F-->FormPage
        linkStyle 24 stroke:red,stroke-width:2px;
    end
    ViewPage--C-->EditBtn--S-->FormPage
    linkStyle 25 stroke:blue,stroke-width:2px;
    linkStyle 26 stroke:green,stroke-width:2px;
    EditBtn--F-->ViewPage  
    linkStyle 27 stroke:red,stroke-width:2px;   
    
 {{< /mermaid >}}

| Symbol     | Action    |
|------------|-----------|
| C          | ClickOn   |
| S          | OnSuccess |
| F          | OnFailure |
| Blue Link  | Click     |
| Green Link | Success   |
| Red Link   | Failure   |


### Flowchart  For  Creation Of Family Types
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    CreateHouseProperty[Create House Property Page]
    subgraph Create Families
        CreationOfFamilies[Create Families]
        AddOwnerFamilyBtn[Add Owner Family + ,Must and Should be create] 
        AddOtherFamilyBtn[Add Other Family + ,May or May not be create]
        OwnHouse{Own House}
        Yes[YES]
    end  
    subgraph Family Form Page
        FormPage[Family Form Page]
        FormPage1[Family Form Page]
        Owner&HeadSame{Owner&Head Same?}
        AddOwnerBtn[Add Owner +,May or May not be create]
        AddHeadBtn[Add Head +,Must and Should be crete]
        AddPersonBtn[Add Person +,May or May not be create]
        Yes2[Yes]
        No[No]
    end 
    subgraph Refer To Citizen
      ReferToCitizen[Refer To Citizen] 
    end   
    
    Start-->CreateHouseProperty
    CreateHouseProperty-->CreationOfFamilies
    CreationOfFamilies-->OwnHouse
    OwnHouse-->Yes-->AddOwnerFamilyBtn
    Yes-->AddOtherFamilyBtn
    OwnHouse--No-->AddOtherFamilyBtn
    
    %%Owner Family
    AddOwnerFamilyBtn--ClickOn AddOwnerFamily-->FormPage
    FormPage-->Owner&HeadSame
    Owner&HeadSame-->Yes2-->AddHeadBtn
    Yes2-->AddPersonBtn
    Owner&HeadSame-->No-->AddHeadBtn
    No-->AddOwnerBtn
    No-->AddPersonBtn
    
    %%OtherFamily
    AddOtherFamilyBtn--ClickOn AddFamily-->FormPage1
    FormPage1-->AddHeadBtn
    FormPage1-->AddPersonBtn
    
    %%Refer To Citizen
    AddHeadBtn--Click on AddHead-->ReferToCitizen
    AddOwnerBtn--Click on AddOwner-->ReferToCitizen
    AddPersonBtn--Click on AddPerson-->ReferToCitizen 
    ReferToCitizen -->End 
     
{{< /mermaid >}}

### Sequence Diagram


{{<mermaid align="center">}}
            sequenceDiagram
              participant SQLite as SQLite Database
              participant ListPage as Create House Property Page: Family List
              participant FormPage as Family Form Page
              participant KVDB as KV Database
              participant ViewPage as Family View Page
              autonumber 
              
              rect rgb(244,244,244)
                  Note right of FormPage: If (Adding new Family or update Family) (1) else { (5) }
                  FormPage->>+KVDB: save Family KV Data in KVDatabase
              end
              rect rgb(244,244,244)
                  ViewPage->>+KVDB: get Family KV Data 
                  KVDB-->>-ViewPage: KV Family Data    
              end  
              rect rgb(244,244,244)
                  Note Left of ViewPage: if (Edit == true) {update family} else {insert family}
                  ViewPage->>+SQLite: updateFamily(Family) (or) insertFamily(Family) 
              end  
              rect rgb(244,244,244)
                  ListPage->>+SQLite: load All Families based on house id
                  SQLite-->>-ListPage: List Of families
              end    
              rect rgb(244,244,244)
                  Note left of ViewPage: View Family Data
                  ViewPage->>+SQLite: fetchFamilyById(id) 
                  SQLite-->>-ViewPage: Family Object
              end   
              rect rgb(244,244,244)
                  Note left of ViewPage: Edit Family Data
                  FormPage->>+SQLite: fetchFamilyById(id) 
                  SQLite-->>-FormPage: Family Object
              end    
              rect rgb(244,244,244)
                  Note right of FormPage: Repeat (1) to (4)
              end
              rect rgb(244,244,244)
                  Note right of SQLite: Repeat (5) and (6)
              end    
{{< /mermaid >}}

## Acceptance Criteria
| Description                                                                                    |
|------------------------------------------------------------------------------------------------|
| Version : 1.0                                                                                  |
| 1. Survey User can able to Create, View, Update, Search, Delete and Sync the Auction Property. |
## Unit Test Cases
| Product Version | UnitTest Id | Description |
|-----------------|-------------|-------------|
| -               | -           | -           |
| -               | -           | -           |

## Security compliance check
1. Only Survey User should Create, View, Update, Delete, Search and Sync the Auction Property.
 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER PERMISSIONs in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
| Feature/Defect ID | Link                                                     | Status |
|-------------------|----------------------------------------------------------|--------|
| GS-0002           | [GS-0002](https://shadkona.atlassian.net/browse/GS-0002) | Closed |


## References
1. [Android Developer Docs](https://developer.android.com/docs)
## Development Estimations
| Release Tag | Feature/Defect ID | Scrum Deatils   | Start date  | End date    |
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




 
