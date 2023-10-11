---
title: User Manual
tags : ["Composing"]
---

## Introduction
User Manual is one of the basic features of the software product. User Manual provides application functionality and app flow details to the survey user. It contains four sections 1.Product Manual, 2.Visual Manual, 3.FAQ (Frequently Asked Questions), and 4.Trouble Shooting. Using **product manual** and **visual manual** sections, the user can gain application knowledge. The user can clarify his doubts using the **FAQ** section. Using the **Trouble Shooting** section user can able to solve the problems what they faced with in the application.  

## Business Assumptions
1. Survey User can able to read product docs and view product videos.
1. Survey Users can able to read FAQ and clarify their doubts.
1. Survey Users can able to solve the problems they faced with the application. 

## Requirements
### Functional Requirements
1. Based on the intent key, we have to fetch the required URL. According to that URL, show the respective manual section page.

### Non-functional Requirements


### Problem Statement
User Manual feature is required to understand the application details, to clarify doubts, and to solve problems faced with application during the survey.

### Design 
1. User Manual page contains four sections 1.Product Manual, 2.Visual Manual, 3.FAQ (Frequently Asked Questions), and 4.Trouble Shooting.
1. Using the product manual section, the user can read product docs.
1. Using the visual manual section, the user can watch videos about the product.
1. The user can clarify his doubts with the **FAQ** section. 
1. Using the **Trouble Shooting** section user can solve the problems he faced with the application.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Side Menu|[Side Menu]({{< ref "side menu" >}})|Parent Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_user_manual_btn|To navigate the user to user manual page|
|uc_product_manual_btn|To navigate the user to product manual page|
|uc_visual_manual_btn|To navigate the user to video tutorial page|
|uc_faq_btn|To navigate the user to frequently asked questions page|
|uc_trouble_shooting_btn|To navigate the user to Trouble Shooting page|

#### KV Database Keys From Context Preferences

|Key Name|
|--------|
|DOC_URL|
|VIDEO_URL|
|FAQ_URL|
|TROUBLE_SHOOTING_URL|

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
|1. Survey User can able to read product docs, watch product videos, clarify doubts and solve problems what they face during the survey.|

## User Experience
### User Manual PAge
{{<mermaid align="left">}}
graph LR
    ProductManualBtn[Product Manual Button]-->VisualManualBtn[Visual Manual Button]-->FAQBtn[FAQ Button]-->TroubleShootingBtn[Trouble Shooting Button] 
{{< /mermaid >}}




### State Machine
{{<mermaid align="left">}}
flowchart TD
    Start((start))
    SideMenu[Side Menu]
    UserManualBtn[User Manual Button]
    UserManualPage[User Manual Page]
    SideMenuBtn[Side Menu Button]
    ProductManualBtn[Product Manual Button]
    ProductManualPage[Product Manual Page]
    VisualManualBtn[Visual Manual Button]
    VisualManualPage[Visual Manual Page]
    FAQBtn[FAQ Button]
    FAQPage[FAQ Page]
    TroubleShootingBtn[Trouble Shooting Button]
    TroubleShootingPage[Trouble Shooting Page]
    ExceptionAlertMessage1>Exception Alert Message]
    ExceptionAlertMessage2>Exception Alert Message]
    ExceptionAlertMessage3>Exception Alert Message]
    End((end))
    %% link 0
    Start-->SideMenu
    subgraph App Side Menu
        %%link 1
        SideMenu--C-->UserManualBtn
        %%link 2
        UserManualBtn--F-->ExceptionAlertMessage1
    end
    subgraph side menu click
        %%link 3
        UserManualPage--C-->SideMenuBtn
        %%link 4
        SideMenuBtn--F-->ExceptionAlertMessage3
    end    
    %%link 5
    SideMenuBtn--S-->SideMenu
    subgraph User Manual Page
        %%link 6
        UserManualBtn--S-->UserManualPage
        %%link 7
        UserManualPage--C-->ProductManualBtn
        %%link 8
        UserManualPage--C-->VisualManualBtn
        %%link 9
        UserManualPage--C-->TroubleShootingBtn
        %%link 10
        UserManualPage--C-->FAQBtn
    end
    subgraph Product Manual
        %%link 11
        ProductManualBtn--S-->ProductManualPage
    end
    subgraph Visual Manual
        %%link 12
        VisualManualBtn--S-->VisualManualPage
    end
    subgraph FAQ
        %%link 13
        FAQBtn--S-->FAQPage
    end
    subgraph Trouble Shooting
        %%link 14
        TroubleShootingBtn--S-->TroubleShootingPage
    end
    %%link 15
    ProductManualBtn--F-->ExceptionAlertMessage2
    %%link 16
    VisualManualBtn--F-->ExceptionAlertMessage2
    %%link 17
    FAQBtn--F-->ExceptionAlertMessage2
    %%link 18
    TroubleShootingBtn--F-->ExceptionAlertMessage2
    %% End
    %%link 20
    ProductManualPage-->End
    %%link 21
    VisualManualPage-->End
    %%link 22
    FAQPage-->End
    %%link 23
    TroubleShootingPage-->End
    %% click representation
    linkStyle 1 stroke:blue,stroke-width:2px;
    linkStyle 3 stroke:blue,stroke-width:2px;
    linkStyle 7 stroke:blue,stroke-width:2px;
    linkStyle 8 stroke:blue,stroke-width:2px;
    linkStyle 9 stroke:blue,stroke-width:2px;
    linkStyle 10 stroke:blue,stroke-width:2px;
    %% success representation
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px;
    linkStyle 12 stroke:green,stroke-width:2px;
    linkStyle 13 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    %% failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 4 stroke:red,stroke-width:2px;
    linkStyle 15 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
    linkStyle 17 stroke:red,stroke-width:2px;
    linkStyle 18 stroke:red,stroke-width:2px;
    
    
    
    
    	
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
No Code Flowchart for this feature.

### Sequence Diagram
{{<mermaid align="left">}}
sequenceDiagram
    participant UserManualPage as User Manual Page
    participant KVDB as KV Database   
    autonumber
    rect rgb(244,244,244)
        UserManualPage->>+KVDB: get values of DOC_URL, VIDEO_URL, FAQ_URL, and TROUBLE_SHOOTING_URL
        KVDB-->>-UserManualPage: values of DOC_URL, VIDEO_URL, FAQ_URL, and TROUBLE_SHOOTING_URL
    end     
{{< /mermaid >}}


## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
|-|-|-|
|-|-|-|

## Security compliance check
Only Survey User should read product docs, watch product videos, clarify doubts, and solve the problems he faced during the survey.

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




 
