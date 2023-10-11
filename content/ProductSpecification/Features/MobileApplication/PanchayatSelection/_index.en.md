---
title: Panchayat Selection
tags : ["Composing"]
---

## Introduction
Panchayat selection is one of the basic features of the software product which contains the data of all the districts names, divisions names, Mandal names, and panchayat names of the Telangana state.
By using this panchayat selection feature we have to know about  in which district, in which division, in which Mandal, and in which panchayat a surveyor surveys. Every survey user should be select all the details of Panchyat Selection before Starts the survey.
## Business Assumptions
1. Panchayat selection feature should be planned at the design phase.
1. The surveyor should be select all Panchayat details one after one. That means users must allow selecting division only after selecting the district. Likewise, the selection of Mandal is allowed only after selecting the division. The same applied to the selection of panchayat also.
1. The order of the Panchayat selection is district,division,mandal,panchyat


## Requirements
### Functional Requirements
1. Before using the panchayat selection  feature user should ***sign-in*** in the application.
1. Steps to the Selection of panchayat :
    1. Firstly the user is required to choose the district(With proper internet connection) after that division names should be loded from the API server which matches the district name.
    1. After loading the division user now required to select the division.
    1. Next the mandal names should be loaded from the API server that matches division and user now required to select the mandal
    1. Next the panchayat names should be loaded from the API server that matches the mandal name and lastly choose the panchayath.

1. After selection of panchayat we need to show the all the details of panchyat in list view.


### Non-functional Requirements
1. Until the survey is completed, the user will be able to select only one panchayat
1. The user selects another panchayat only after the completion of the initial panchayat survey.
1. Multiple users can be  select the same panchayat to the  survey.

### Problem Statement
The Panchyat selection  feature is required to know that in which district,in which division,in which mandal and in which panchayat user surveys. 

### Design
1. Panchyat selection feature has two pages one is panchyat selection form another one is panchyat info.
1. Panchyat selection form contains District  ,Division ,Mandal and Panchyat fields which are type of ***Spinner***.
1. Panchyat selection form also contain ***Continue Survey*** Button, which is used to start the survey after choosing panchayat selection.
1. Panchyat Info page contains District, Division, Mandal and Panchyat fields which are a type of ***Text View*** to show the information about selected panchayat.
1. Panchyat Info page also contains the ***Panchayat Data*** button which used to take the details of Sarpanch and Secretary Details.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Sign In|[Login]({{< ref "Login" >}})|You can only use the panchayat selection feature when you first ***sign-in***  in to the application.|
|Side Menu|[Side Menu]({{< ref "Side Menu" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_panchayat_data|To take  the sarpanch and secretary data of the selected panchayat.|
|uc_continue_survey| To continue the survey After the success of Panchayat Selection. |

#### Shared Preference Keys
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|
|stateId|YES|NA|a-zA-Z0-9, maxlen=128|stateId String|NA|NA|NA|NO|NO|NO||
|stateName|YES|NA|a-zA-Z0-9, maxlen=128|stateName String|NA|NA|NA|NO|NO|NO||
|distId|YES|NA|a-zA-Z0-9, maxlen=128|distId String|NA|NA|NA|NO|NO|NO||
|distName|YES|NA|a-zA-Z0-9, maxlen=128|distName String|NA|NA|NA|NO|NO|NO||
|divId|YES|NA|a-zA-Z0-9, maxlen=128|divId String|NA|NA|NA|NO|NO|NO||
|divName|YES|NA|a-zA-Z0-9, maxlen=128|divName String|NA|NA|NA|NO|NO|NO||
|mandalId|YES|NA|a-zA-Z0-9, maxlen=128|mandalId String |NA|NA|NA|NO|NO|NO||
|mandalName|YES|NA|a-zA-Z0-9, maxlen=128|mandalName String|NA|NA|NA|NO|NO|NO||
|panchayatId|YES|NA|a-zA-Z0-9, maxlen=128|panchayatId String|NA|NA|NA|NO|NO|NO||
|panchayatName|YES|NA|a-zA-Z0-9, maxlen=128|panchayatName String|NA|NA|NA|NO|NO|NO||

#### Feature Permission
No feature permission for this login feature.

|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|

## Acceptance Criteria
1. Anyone who sign-in to this application can view panchayat selection page.
1. Each user can fill the panchayat selection only once. If another panchayat needs to be selected, the panchayat survey has to be completed first.

## User Experience
### Panchayat Selection from Side menu
{{<mermaid align="left">}}
graph LR
    ContinueSurveyBtn[Continue Survey]
{{< /mermaid >}}

{{<mermaid align="left">}}
graph LR
    PanchayatDataBtn[Panchayat Data]
{{< /mermaid >}}


### state machine
{{<mermaid align="center">}}
flowchart TD
    SideMenuPage((  Side Menu Page ))
	PanchyatFragmentBtn[Panchayat Selection Btn]
	StartContinueSurveyFragmentBtn[Start/Continue Survey Btn]
	PanchayatSelectionPage[Panchayat selection form page ]
	PanchayatInfoPage[Panchyat info page]
	ContinueSurveyBtn[Continue Survey Button]
	PanchayatDataBtn[Panchayat Data Button]
	SurveyPage[Start/Continue Survey Page]
	PanchyatDataListPage[Panchyat Staff List Page]

	SideMenuPage--C-->PanchyatFragmentBtn
	linkStyle 0 stroke:blue,stroke-width:2px,color:black;
	SideMenuPage--C-->StartContinueSurveyFragmentBtn
	linkStyle 1 stroke:blue,stroke-width:2px,color:black;
	PanchyatFragmentBtn--SBSP-->PanchayatSelectionPage
	linkStyle 2 stroke:yellow,stroke-width:2px,color:black;
	StartContinueSurveyFragmentBtn--SBSP-->PanchayatSelectionPage
	linkStyle 3 stroke:yellow,stroke-width:2px,color:black;
	PanchyatFragmentBtn--SASP-->PanchayatInfoPage
	linkStyle 4 stroke:pink,stroke-width:2px,color:black;
    StartContinueSurveyFragmentBtn--SASP-->SurveyPage
    linkStyle 5 stroke:pink,stroke-width:2px,color:black;
    PanchyatFragmentBtn--F-->SideMenuPage
    linkStyle 6 stroke:red,stroke-width:2px,color:black;
    StartContinueSurveyFragmentBtn--F-->SideMenuPage
    linkStyle 7 stroke:red,stroke-width:2px,color:black;
    PanchayatSelectionPage--C-->ContinueSurveyBtn
    linkStyle 8 stroke:blue,stroke-width:2px,color:black;
    PanchayatInfoPage--C-->PanchayatDataBtn
    linkStyle 9 stroke:blue,stroke-width:2px,color:black;
    ContinueSurveyBtn--S-->SurveyPage
    linkStyle 10 stroke:green,stroke-width:2px,color:black;
    PanchayatDataBtn--S-->PanchyatDataListPage
    linkStyle 11 stroke:green,stroke-width:2px,color:black;
    ContinueSurveyBtn--F-->PanchayatSelectionPage
    linkStyle 12 stroke:red,stroke-width:2px,color:black;
    PanchayatDataBtn--F-->PanchayatInfoPage
    linkStyle 13 stroke:red,stroke-width:2px,color:black;

{{< /mermaid >}}

| Symbol| Description|Color Indication|
|--|--|--|
| C| OnClick| Blue|
| S| OnSuccess| Green|
| F| OnFailure| Red|
|SBSP|Sucess Before Selection of Panchayat|Yellow|
|SASP|Sucess After Selection of Panchayat|Pink|


### Panchayat Selection flow : offline and online
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%

flowchart TD
    start((start))
    sideMenuPage[Side Menu]
    clickOn{Click On}
    clickOnStart/ContinueSurveyBtn[ Click on Continue/Start Survey Button ]
    currentPanchayatIdCondition1{ Current Panchayat id is null?}
    currentPanchayatIdCondition2{  Current Panchayat id is null?}

    checkNetworkConnection{Internet Connection}
    checkNetworkConnection1{Internet Connection}
    checkNetworkConnection2{Internet Connection}
    checkNetworkConnection3{Internet Connection}

    showMessageNetworkConnection>Message : Please Connect With Internet]
    showMessageNetworkConnection1>Message : Please Connect With Internet]
    showMessageNetworkConnection2>Message : Please Connect With Internet]
    showMessageNetworkConnection3>Message : Please Connect With Internet]

    showErrMsg>show error message]
    showErrMsg1>show error message]
    showErrMsg2>show error message]
    showErrMsg3>show error message]




    panchayatSelectionPage[Panchyat Selection Page]
    panchayatInfoPage[Panchayat Info Page]
    surveyPage[ Survey Page ]
    failedTokenCndtn{Failed token !=null}
    failedTokenUnsucessful{Failed token equals to unsucessful}
    invokeAutAPI{ invokeAuthApi }
    invokeContext[invoke context]
    loginPage[Login Page]
    showAPIErrMsg>Show Message : API Error Message ]

    loadAllDistricts[Load ALl Districts]
    loadDivisions[Load All Divisions With respect to District]
    loadMandals[Load All Mandals With respect to Division]
    loadPanchayats[Load All Panchayatas With respect to Mandal]

    loadAllDistrictsFrmAPIServer{ Load All Dstricts From API Server. }
    loadAllDivisionsFrmAPIServer{ Load All Divisions From API Server. }
    loadAllMandalsFrmAPIServer{ Load All Mandals From API Server. }
    loadAllPanchayatsFrmAPIServer{ Load All Panchayats From API Server. }

    selectDistrict[Select District From Spinner]
    selectDivision[Select Division From Spinner]
    selectMandal[Select Mandal From Spinner]
    selectPanchayat[Select Panchyat From Spinner]

    storeAllDistricts[Store All districts in Array]
    storeAllDivisions[Store All divisions in Array]
    storeAllMandals[Store All mandals in Array]
    storeAllPanchayats[Store All panchayats in Array]

    districtSelectioncondition{Is District Selected?}
    districtOrDivisionSelectioncondition{Is District or Division Selected?}
    districtOrDivisionOrMandalSelectioncondition{Is District or Division or Mandal Selected?}
    districtOrDivisionOrMandalOrPanchayatSelectioncondition{Is District or Division or Mandal or Panchyat Selected?}

    loadAlldeatilsOfPanchayatFromsharedPrefrence[load all details of Panchayat From SharedPreference]
    displayDetails[Display the panchayat details In Info Page]

    End((end))
    End1((end))
    End2((end))
    End3((end))




    start-->sideMenuPage
    sideMenuPage-->clickOn
    clickOn--Panchayat-->currentPanchayatIdCondition1
    clickOn--start/continue Survey-->currentPanchayatIdCondition2
    currentPanchayatIdCondition2--true-->panchayatSelectionPage
    currentPanchayatIdCondition2--false-->surveyPage-->End3
    panchayatSelectionPage-->loadAllDistricts-->checkNetworkConnection
    checkNetworkConnection--true-->loadAllDistrictsFrmAPIServer
    checkNetworkConnection--false-->showMessageNetworkConnection
    loadAllDistrictsFrmAPIServer--response==200-->storeAllDistricts
    subgraph One
    response==401-->failedTokenCndtn
    response==400-->showAPIErrMsg
    failedTokenCndtn--true-->failedTokenUnsucessful
    failedTokenCndtn--false-->invokeAutAPI
    failedTokenUnsucessful--true-->loginPage-->End2
    invokeAutAPI--response==200-->invokeContext
    invokeAutAPI--response==401-->failedTokenCndtn
    end
    loadAllDistrictsFrmAPIServer---response!=200-->One


    storeAllDistricts-->selectDistrict
    selectDistrict-->loadDivisions
    loadDivisions-->checkNetworkConnection1
    checkNetworkConnection1--true-->loadAllDivisionsFrmAPIServer
    checkNetworkConnection1--false-->showMessageNetworkConnection1
    loadAllDivisionsFrmAPIServer--response==200-->storeAllDivisions
    loadAllDivisionsFrmAPIServer---response!=200-->One
    storeAllDivisions-->selectDivision

    selectDivision-->districtSelectioncondition
    districtSelectioncondition--true-->loadMandals
    districtSelectioncondition--false-->showErrMsg
    loadMandals-->checkNetworkConnection2
    checkNetworkConnection2--true-->loadAllMandalsFrmAPIServer
    checkNetworkConnection2--false-->showMessageNetworkConnection2
    loadAllMandalsFrmAPIServer--response==200-->storeAllMandals
    loadAllMandalsFrmAPIServer---response!=200-->One
    storeAllMandals-->selectMandal
    selectMandal-->districtOrDivisionSelectioncondition
    districtOrDivisionSelectioncondition--false-->showErrMsg1
    districtOrDivisionSelectioncondition--true-->loadPanchayats
    loadPanchayats-->checkNetworkConnection3
    checkNetworkConnection3--true-->loadAllPanchayatsFrmAPIServer
    checkNetworkConnection3--false-->showMessageNetworkConnection3
    loadAllPanchayatsFrmAPIServer--response==200-->storeAllPanchayats
    loadAllPanchayatsFrmAPIServer---response!=200-->One

    storeAllPanchayats-->selectPanchayat
    selectPanchayat-->districtOrDivisionOrMandalSelectioncondition
    districtOrDivisionOrMandalSelectioncondition--false-->showErrMsg2
    districtOrDivisionOrMandalSelectioncondition--true-->clickOnStart/ContinueSurveyBtn
    clickOnStart/ContinueSurveyBtn-->districtOrDivisionOrMandalOrPanchayatSelectioncondition
    districtOrDivisionOrMandalOrPanchayatSelectioncondition--true-->SurveyPage-->End1
    districtOrDivisionOrMandalOrPanchayatSelectioncondition--false-->showErrMsg3




    currentPanchayatIdCondition1--false-->panchayatInfoPage
    currentPanchayatIdCondition1--true-->panchayatSelectionPage
    panchayatInfoPage-->loadAlldeatilsOfPanchayatFromsharedPrefrence
    loadAlldeatilsOfPanchayatFromsharedPrefrence-->displayDetails-->End













{{< /mermaid >}}



### Panchayat Selection Page & GS-Cloud Operations
{{<mermaid align="center">}}
sequenceDiagram
    participant SurveyPage as Survey Page
    participant KvDb as KV Data Base
    participant SQLite as SQLite Database
    participant PanchayatSelectionPage as Panchayat Selection Page
    participant Net as Network Utils
    participant cloud as GS-Cloud
    autonumber

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+Net: Check Internet , GET /api/1/District/list Load All  Districts
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : GET /api/1/District/list Load All  Districts
        cloud-->>-PanchayatSelectionPage: RES 200
        Note over Net: If response equals to 401  { go to step ( 17 to 22 ) }
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+Net: Check Internet , GET /api/Division/list Load All  Divisions
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : GET /api/Division/list Load All  Divisions
        cloud-->>-PanchayatSelectionPage: RES 200
        Note over Net: If response equals to 401  { go to step ( 17 to 22 ) }
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+Net: Check Internet , GET/api/Mandal/list Load All  Mandals
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : GET/api/Mandal/list Load All  Mandals
        cloud-->>-PanchayatSelectionPage: RES 200
        Note over Net: If response equals to 401  { go to step ( 17 to 22 ) }
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+Net: Check Internet , GET /api/Panchayat/list Load All  Panchayats
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : GET /api/Panchayat/list Load All  Panchayats
        cloud-->>-PanchayatSelectionPage: RES 200
        Note over Net: If response equals to 401  { go to step ( 17 to 22 ) }
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+SQLite: load single user with given UserId
        SQLite-->>PanchayatSelectionPage: User Object
        PanchayatSelectionPage->>+Net: Check Internet , POST /api/login Authentication invokeAuthApi
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : POST /api/login Authentication
        cloud-->>-PanchayatSelectionPage: RES 200
        Note over Net: If response equals to 200  { go to step ( 23 to 26 ) }
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+Net: Check Internet , GET /api/1/CtxDto Context API Call
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : GET /api/1/CtxDto Context API Call
        cloud-->>-PanchayatSelectionPage: RES 200
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+Net: Check Internet , GET /api//PanchayatSurveyStart PanchyatStartSurvey
        Net--x-PanchayatSelectionPage: F : Connection Error
        PanchayatSelectionPage->>+cloud: S : GET /api//PanchayatSurveyStart PanchyatStartSurvey
        cloud-->>-PanchayatSelectionPage: RES 200
        Note over Net: If response equals to 200  { go to step ( 31 )
      end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+KvDb: Insert All Panchayat Details
     end

     rect rgb(244,244,244)
        PanchayatSelectionPage->>+SurveyPage: On Panchyat Selection Success
     end







{{< /mermaid >}}

### Panchayat Info Page & KVDB Operations

{{<mermaid align="center">}}
sequenceDiagram
    participant KvDb as KV Data Base
    participant PanInf as Panchayat Info Page

    rect rgb(244,244,244)
            PanInf->>+KvDb: Get panchayat details
            KvDb-->>+PanInf:Displaying the details

          end

{{< /mermaid >}}

## Security compliance check
1. Only login user can able to view the Panchayat Selection Feature.
## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Panchayat Selection in the User Manual. It's scope is limited to Developer Technical Document

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0002|[GS-0002](https://shadkona.atlassian.net/browse/GS-0002)|Closed|


## References
1. [Android Developer Docs](https://developer.android.com/docs)

## Development Estimations
|Release Tag|Feature/Defect ID|Scrum Details|Start date|End date|
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













