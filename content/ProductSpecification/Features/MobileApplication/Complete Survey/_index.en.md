---
title:  Complete Survey
tags : ["Composing"]
---

## Introduction
In complete survey module Survey Executive after successful completion of surveying all the modules(i.e House,Auction,Advertisement,Kolagaram,TradeLicense,VacantLand and Locked Property) and Successfully Uploaded or synced the data into the GS-Cloud, He/She has to intimate to the organization that survey in this particular Panchayat was successful.After Completion of this module only Survey Executive able to select other pachayat in order to contine survey in that PAnchayat.

## Business Assumptions
1. Complete Survey feature should be planned at design phase.
1. User should be in the panchayat level to complete the survey.
1. User E-Mail address and Mobile Number are required to complete the survey.


## Requirements
### Functional Requirements
1. To complete survey Survey User should upload all the data to the GS-Cloud.
1. User should Enter the Mobile Number and E-mail address which was given at the time of Sign-In.
1. Time limit should be set to OTP ,after previous OTP is expired user can get another OTP.  

### Non-functional Requirements
1. Multiple users can sync/upload different properties in the same panchayat and can complete survey.


### Problem Statement
With the help of Complete Survey module Organization can acknowledge how many panchayats survey is so for completed.  

### Design 
1. Survey User can go to Upload Data module if all the properties are not synced from the Complete Survey Module.
1. Survey User can get another OTP if previous one is expired. 

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Side Menu|[Side Menu]({{< ref "side menu" >}})|Parent Page|


#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_view_complete_survey|To view the Complete Survey Page|
|uc_complete_complete_survey|To view the Complete the survey with the help of OTP|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|NA|NA|NA|NA|NA|NA|NA|NA|NA||



#### Feature Permission

|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|

## Acceptance Criteria
1. Only the Users who are register as survey executive can Complete the Survey

## User Experience
### To continue completion 
{{<mermaid align="left">}}
graph LR
    OKBtn[OK]
{{< /mermaid >}}
### If all the data is not Uploaded to the Server
{{<mermaid align="left">}}
graph LR
    UploadBtn[Upload]
{{< /mermaid >}}
### In Complete Survey Page
{{<mermaid align="left">}}
graph LR
    ConfirmBtn[Confirm]
    ResendBtn[Resend]
{{< /mermaid >}}
### State Machine

{{<mermaid align="left">}}
flowchart TD
    start((Start))
	SideMenuBtn[SideMenu Fragment]
	CompleteSurveyBtn[Complete Survey]
	CompleteFormPage[Complete Survey Form Page]
	SurveyOtpPage[Get SMS OTP Page]
	OkBtn[OK Button]
	UploadBtn[Upload Data Button]
	ConfirmBtn[Confirm Button]
	ResendBtn[Resend OTP]
	UploadPage[Upload Data Page]
	start-->SideMenuBtn
	subgraph SideMenu
	SideMenuBtn--C-->CompleteSurveyBtn
	end  
	subgraph Complete Form Page
	CompleteSurveyBtn--S-->CompleteFormPage
	CompleteSurveyBtn--F-->SideMenuBtn
	CompleteFormPage--Data Uploaded-->OkBtn
	CompleteFormPage--Data NotUploaded-->UploadBtn
	end
	subgraph Survey OTP Page
	OkBtn--C-->SurveyOtpPage
	SurveyOtpPage--got OTP-->ConfirmBtn
	SurveyOtpPage--Not get OTP-->ResendBtn
	ConfirmBtn--S-->CompleteFormPage
	ConfirmBtn--F-->SurveyOtpPage
	end 
	subgraph Upload Module
	UploadBtn--C-->UploadPage
	end
	%%For Success Operations
	linkStyle 2 stroke:green,stroke-width:2px;
	linkStyle 9 stroke:green,stroke-width:2px;
	%%For OnClick Operations
    linkStyle 1 stroke:blue,stroke-width:2px;
    linkStyle 6 stroke:blue,stroke-width:2px;
    linkStyle 11 stroke:blue,stroke-width:2px;
    %%For Failure Operations
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    %%For Other Operations
    linkStyle 0 stroke:yellow,stroke-width:2px;
    linkStyle 4 stroke:yellow,stroke-width:2px;
    linkStyle 5 stroke:yellow,stroke-width:2px;
    linkStyle 7 stroke:yellow,stroke-width:2px;
     linkStyle 8 stroke:yellow,stroke-width:2px;
    
    
{{< /mermaid >}}

### Flow of the Dashboard Module
{{<mermaid align="center">}}
flowchart
    Start((start))
    UploadDataCheck{check all the data synced or not}
    UploadBtn[Upload Button]
    OkBtn[OK Button]
    UploadDataModule[go to Upload Page]
    CompleteSurvey[Complete survey OTP Page]
    InternetCheck{Check Internet Connection}
    gotOTP[got OTP, enter it]
    InternetError[Check your Internet Connection]
    ConfirmBtn[Confirm Button]
    ResendBtn[Resend Button]
    LoginPage[Login Page]
    end1((end))
    Start-->UploadDataCheck
    UploadDataCheck--NO-->UploadBtn
    UploadBtn--c-->UploadDataModule
    UploadDataModule-->end1
    UploadDataCheck--YES-->OkBtn
    OkBtn--c-->CompleteSurvey
    CompleteSurvey-->InternetCheck
    InternetCheck--YES-->gotOTP
    gotOTP--s-->ConfirmBtn
    ConfirmBtn--s-->LoginPage
    LoginPage-->end1
    ConfirmBtn--f-->CompleteSurvey
    gotOTP--f-->ResendBtn
    ResendBtn--c-->CompleteSurvey
    InternetCheck--NO-->InternetError
    InternetError-->InternetCheck
{{< /mermaid >}}


### Sequence of actions in Dashboard module
{{<mermaid align="center">}}
sequenceDiagram
    participant M as Mobile
    participant SQL as SQLite
    participant Net as Network Utils
    participant FormPage as Complete Survey
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
         M->>SQL: Check all the data got synced 
         Note right of M: If (yes) go to Complete survey page  else { go to upload page }   
    end 
    rect rgb(244,244,244)
          M->>+Net: Check Internet , GET /api/1/Complete survey Page
          Net--x-M: F : Connection Error
          M->>+FormPage: S : go to Complete survey Page 
     end  
     rect rgb(244,244,244)
          cloud-->>-FormPage: List Of Kolagaram 
     end 
     
    
{{< /mermaid >}}


## Security compliance check
1. Nothing specific found

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER ROles in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0002|[GS-0002](https://shadkona.atlassian.net/browse/GS-0002)|Closed|


## References
1. [Android Developer Docs](https://developer.android.com/docs)

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




 
