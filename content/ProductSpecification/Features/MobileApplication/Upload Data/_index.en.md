---
title: Upload Data
tags : ["Composing"]
---

## Introduction
Upload Data is an important feature in panchayat Telangana Survey application. The main goal of the Upload feature is to upload all taxable properties to GS-Cloud Server. The upload page contains switch buttons that are used to upload property data to GS-Cloud.
After clicking a particular property switch button respective properties uploaded to GS-Cloud.


## Business Assumptions
1. Upload Data feature should be planned at the design phase.
1. Survey User can able to upload the properties to GS-Cloud.

## Requirements
### Functional Requirements
1. The properties which have survey pending value as false only synced to Gs-Cloud.
1. Once a property is uploaded to Gs-Cloud, the user is not allowed to update it.
1. After property uploaded, set uploaded property data sync values as 1 to show property uploaded in UI (green color horizontal line indicates property successfully uploaded to Gs-Cloud.).

### Non-functional Requirements
1. Multiple users can sync properties in the same panchayat or different panchayats.
1. Two survey users created same property. While uploading only one property will sync among all users based on who syncs first.


### Problem Statement
Upload Data feature is required to upload all the Citizen, House, Auction, Advertisement, TradeLicense, Kolagaram, Vacant Land, and Locked properties to Gs-Cloud Server.

### Design 
1. Upload Data page contains eight property card. Each card has tile, uploaded records count, survey pending count, Total records count, and switch button.
1. After clicking a particular switch button respective properties are uploaded to the GS-Cloud server.
1. The properties which are uploaded to the server have green color horizontal line in list page.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Side Menu|[Side Menu]({{< ref "side menu" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_upload_house_switch_btn|To upload the house properties to GS-Cloud|
|uc_upload_auction_switch_btn|To upload the auction properties to GS-Cloud|
|uc_upload_advertisement_switch_btn|To upload the advertisement properties to GS-Cloud|
|uc_upload_trade_license_switch_btn|To upload the trade license properties to GS-Cloud|
|uc_upload_kolagaram_switch_btn|To upload the kolagaram properties to GS-Cloud|
|uc_upload_locked_property_switch_btn|To upload the locked properties to GS-Cloud|
|uc_upload_vacant_land_switch_btn|To upload the vacant land properties to GS-Cloud|
|uc_upload_panchayat_data_switch_btn|To upload the panchayat data to GS-Cloud|
|uc_upload_green_color|To show the particular property uploaded to the Gs-Cloud server successfully|
|uc_upload_red_color|To show the particular property not uploaded to the Gs-Cloud server|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|KV Database Key|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|---------------------------------|------------|------------------------|------|------|------|----|----|------|-------|
|-|-|-|-|-|-|-|-|-|-|-|-|-|


#### ENUM CONSTANTS
No Enum Constants for this feature.



#### Feature Permission
|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|


#### Constraints
|Constraint|Key|
|----------|----|
|-|-|


## Acceptance Criteria
|Description|
|-------------|
|Version : 1.0|
|1. Survey User can able to Sync the House, Auction, Advertisement, TradeLicense, Kolagaram, Vacant Land, and Locked properties Data to Gs-Cloud.|

## User Experience
### Upload Data Page
{{<mermaid align="center">}}
graph TD
    House[House Switch Button]---Auction[Auction Switch Button]---Advertisement[Advertisement Switch Button]---Trade[Trade License Switch Button]---Kolagaram[Kolagaram Switch Button]---LockedProperty[LockedProperty Switch Button]---VacantLand[VacantLand Switch Button]---PanchayatStaffData[Panchayat Staff Data Switch Button]
{{< /mermaid >}}



### State Machine
{{<mermaid align="center">}}
flowchart TD
	Start((start))
	End((end))
	SideMenu[Side Menu]
	UploadDataBtn[Upload Data Button]
	UploadDataPage[Upload Data Page]
	UploadSwitchBtn[Upload Switch Button]
	UploadedRecordsCountInc[Uploaded Records Count Change]
	showMessageExceptionAlert>Show Exception Alert]
	Start-->SideMenu
	SideMenu--C-->UploadDataBtn
	UploadDataBtn--S-->UploadDataPage
	UploadDataBtn--F-->showMessageExceptionAlert
	UploadDataPage--C-->UploadSwitchBtn
	UploadSwitchBtn--S-->UploadedRecordsCountInc
	UploadSwitchBtn--F-->showMessageExceptionAlert
	UploadedRecordsCountInc-->End
	showMessageExceptionAlert-->End
	%%For click Representation
    linkStyle 1 stroke:blue,stroke-width:2px;
    linkStyle 4 stroke:blue,stroke-width:2px;
    %%For success Representation
	linkStyle 2 stroke:green,stroke-width:2px;
	linkStyle 5 stroke:green,stroke-width:2px;
	%%For fail Representation
	linkStyle 3 stroke:red,stroke-width:2px;
	linkStyle 6 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|ClickOn|
|S|OnSuccess|
|F|OnFailure|
|Blue Link|Click|
|Green Link|Success|
|Red Link|Failure|



### Flowchart
**Below flow is applied for House, Auction, Advertisement, TradeLicense, Kolagaram, Locked Property, vacantLand and panchayat Data.**
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    SideMenu[Side Menu]
    DataUploadPage[Data Upload Page]
    LoadUserFromDB[Load User From SQLite DB]
    GetAllPropertiesCount[get All Properties Count From SQLite Database]
    SetPropertiesCount[Set Properties Count to UI Labels]
    SwitchButtonClick{Switch Button Click}
    FetchTradeLicenseObjectData[Fetch TradeLicense Object From SQLite Database]
    SetTradeLicenseSwitchButtonOff1[Set TradeLicense Switch Button Off]
    TradeLicenseCheck{TradeLicense}
    InternetCheck1{Internet Connected}
    InternetCheck2{Internet Connected}
    InternetCheck3{Internet Connected}
    ApiCallSyncTradeLicense[API Call: syncTradeLicense]
    Response1{Response}
    Response2{Response}
    Response3{Response}
    setDataSyncValueForTradeLicense[set DataSync Value as 1 for uploaded TradeLicense property]
    SetTradeLicenseSwitchButtonOff2[Set TradeLicense Switch Button Off]
    FailedToken1{Failed Token}
    FailedToken2{Failed Token}
    FaildTokenEqualCheck1{FailedToken == UNSUCCESS_TOKEN}
    FaildTokenEqualCheck2{FailedToken == UNSUCCESS_TOKEN}
    LoginPage1[Navigate to Login Page]
    LoginPage2[Navigate to Login Page]
    ApiCallLogin[API Call: login]
    ApiCallGetContext[API Call: getContext]
    CheckMethodLoader{checkMethodLoader}
    RepeatSyncTradeLicenseApiCall[Repeat Sync TradeLicense Api Call]
    End((end))
    %%Connection links
    subgraph side menu
    Start-->SideMenu
    SideMenu--Click Uplode Data-->DataUploadPage
    end
    subgraph upload Data Page
        DataUploadPage-->LoadUserFromDB
        LoadUserFromDB-->GetAllPropertiesCount
        GetAllPropertiesCount-->SetPropertiesCount
        SetPropertiesCount-->SwitchButtonClick
        SwitchButtonClick--Trade Switch-->FetchTradeLicenseObjectData
        FetchTradeLicenseObjectData-->TradeLicenseCheck
        TradeLicenseCheck--Not NULL-->InternetCheck1
        TradeLicenseCheck--NULL-->SetTradeLicenseSwitchButtonOff1
        InternetCheck1-->ApiCallSyncTradeLicense
    end
    subgraph in API Call syncTradeLicense
        ApiCallSyncTradeLicense-->Response1
        Response1--==401-->FailedToken1
        Response1--Other-->SetTradeLicenseSwitchButtonOff2
        FailedToken1--Not NULL-->FaildTokenEqualCheck1
        FaildTokenEqualCheck1--true-->LoginPage1
        FailedToken1--NULL-->InternetCheck2
        InternetCheck2-->ApiCallLogin
    end
    subgraph set
    Response1--==200-->setDataSyncValueForTradeLicense
    end
    setDataSyncValueForTradeLicense-->FetchTradeLicenseObjectData
    LoginPage1-->End
    subgraph in API Call login
        ApiCallLogin-->Response2
        Response2--==401-->FailedToken2
        FailedToken2--Not NULL-->FaildTokenEqualCheck2
        FaildTokenEqualCheck2--true-->LoginPage2 
        Response2--==200-->InternetCheck3
        InternetCheck3-->ApiCallGetContext
    end
    LoginPage2-->End
    subgraph in API Call getContext
        ApiCallGetContext-->Response3
        Response3-- ==200 -->CheckMethodLoader
        CheckMethodLoader-- == TRADE_LICENSE_PROP_SYNC-->RepeatSyncTradeLicenseApiCall
    end
    RepeatSyncTradeLicenseApiCall-->End
      
{{< /mermaid >}}


### Sequence Diagram
{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant UploadPage as Upload Data Page
    participant Net as Network Utils
    participant cloud as GS-Cloud
    autonumber  
    rect rgb(244,244,244)
        UploadPage->>+SQLite: loadOneTradeLicense
        SQLite-->>-UploadPage: TradeLicense Object
    end
    rect rgb(244,244,244)
        Note Right of UploadPage: if (tradeLicense!=NULL) else { stop }
        UploadPage->>+Net: Check Internet , POST /api/1/Trade syncTradeLicense
        Net--x-UploadPage: F : Connection Error
        UploadPage->>+cloud: S : POST /api/1/Trade syncTradeLicense
        cloud-->>-UploadPage: RES 200 
    end    
    rect rgb(244,244,244)
        Note right of UploadPage: if(Response==200) {repeat 1 to 6} else {go to 7}
        UploadPage->>+Net: Check Internet , POST /api/login login
        Net--x-UploadPage: F : Connection Error
        UploadPage->>+cloud: S : POST /api/1/login login
        cloud-->>-UploadPage: RES 200
    end
    rect rgb(244,244,244)
        Note right of UploadPage: if(Response==200)
        UploadPage->>+Net: Check Internet , POST /api/getContext getContext
        Net--x-UploadPage: F : Connection Error
        UploadPage->>+cloud: S : POST /api/1/getContext getContext
        cloud-->>-UploadPage: RES 200
        Note Right of UploadPage: Repeat (3) to (6)
    end                 
{{< /mermaid >}}

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
1. Only Survey User should Sync the House, Auction, Advertisement, TradeLicense, Kolagaram, Vacant Land, and Locked properties Data to Gs-Cloud.

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER ROles in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


## References

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




 
