---
title: Profile Picture
tags : ["Composing"]
---

## Introduction
Profile Picture is one of the features of the software product. Profile Picture feature will provide the option to change the profile picture of the logged in user.

## Business Assumptions
Profile Picture Feature should be planned at the design phase and updates at the run time based on the requirement.

## Requirements
### Functional Requirements
1. User of any level can change his profile picture.
1. User should be log in to change his profile picture.
1. User need not have any permission to change his profile picture.

### Non-functional Requirements
1. Profile Picture should be clear and well.

### Problem Statement
1. Profile Picture is required to change the profile picture of logged in user.

### Design 
1. Size of profile picture should not be greater than 3 MB.	
1. User can add or change his profile picture at any time.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|User|[gs0004-users]({{< ref "gs0004-users" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_change_profile_picture|To change the profile picture|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|----|
|profilePic|YES|NA|Attachment,Allowed JPG, PNG files only. Maximum size 3 MB|@Column(name = "pic", length = 36, nullable = true)|pic varchar(36) DEFAULT NULL|NO|YES|NO|NO|NO||

#### ENUM CONSTANTS


#### Feature Permission
|Permission code|Action|
|---------------|-------|
|||


#### Constraints
|Constraint|Key|
|----------|----|
|||

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|||

## User Experience
1. Update page based on the standard UX Listing Template

### List Page Buttons



### State Machine
{{<mermaid align="left">}}
flowchart TD
	ProfilePictureMenu((Profile Picture Menu))
	UpdatePage((Update Page))
    ErrorPage((Error Page))
    DashboardPage((Dashboard Page))
    Stop((Stop))
	Start((Start))
	Start-->ProfilePictureMenu
	ProfilePictureMenu-->ErrorPage
	ProfilePictureMenu--U-->UpdatePage
	UpdatePage--S-->UpdatePage
	UpdatePage--B-->DashboardPage	
	ErrorPage-->Stop
    %%For success Representation
    linkStyle 2 stroke:green,stroke-width:2px;
    linkStyle 3 stroke:#cc33ff,stroke-width:2px;
    linkStyle 4 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 1 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|U|Update|
|V|View|
|F|Failure|
|B|Back|
|S|Submit|
|SB|Submit or Back|
|Green Arrow|Success|
|Red Arrow|Failure|
|Pink Arrow|Success or Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant ProfilePictureMenu as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        ProfilePictureMenu->>+Net: Check Internet, GET /app/User/profilePic/update/form UpdateFormPage
        Net--x-ProfilePictureMenu: F : Connection Error
        ProfilePictureMenu->>+cloud: S : GET /app/User/profilePic/update/form UpdateFormPage
        cloud-->>-ProfilePictureMenu: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        ProfilePictureMenu->>+Net: Check Internet, POST /app/User/profilePic/update Update
        Net--x-ProfilePictureMenu: F : Connection Error
        ProfilePictureMenu->>+cloud: S : POST /app/User/profilePic/update Update
        cloud-->>-ProfilePictureMenu: RES: Change Profile Picture Successful
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Update |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_500 **Negative Test Cases:** ut_n_u_GSTS_WEB_USERACCOUNT_501 |**Positive Test Cases:** Updating User Profile Pic with Authorised User **Negative Test Cases:** 1.Updating User Profile Pic without DB Connection| **pic**|1|0|1|testAuthorisedUserChangeProfilePic, testAuthorisedUserChangeProfilePicWithoutDBConnection|
|1.0| Update Form|**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_605 **Negative Test Cases:** ut_n_u_GSTS_WEB_USERACCOUNT_606 |**Positive Test Cases:** Open User Pic Update Form with Authorised User **Negative Test Cases:** Open User Pic Update Form without DB Connection| N/A|1|1|2|testAuthorisedUserOpenUserPicUpdateForm, testAuthorisedUserOpenUserPicUpdateFormWithoutDBConnection|


#### UnAuthorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Update |ut_n_u_GSTS_WEB_USERACCOUNT_503|Unauthorised user does not have permission to change the profile pic| **pic**|1|N/A|1|testUnAuthorisedUserChangeProfilePic|

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Profile Picture should be provided in the User Manual.

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




 
