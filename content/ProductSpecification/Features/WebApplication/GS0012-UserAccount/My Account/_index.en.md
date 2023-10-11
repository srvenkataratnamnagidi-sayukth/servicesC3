---
title: My Account
tags : ["Composing"]
---

## Introduction
My Account is one of the basic features of the software product. My account feature will show all the details of the login user. And the details will be updated through my account update feature. 

## Business Assumptions
My Account Feature should be planned at the design phase and updates to the user account information at the run time based on the requirement.

## Requirements
### Functional Requirements
1. My Account feature is accessible at all levels of organization.
1. Login User details will be updated using My Account feature.

## Non-functional Requirements
My Account feature has view and update features only.

### Problem Statement
My Account feature is required to view and update the login user information.

### Design 
1. Each My account has  First Name, Surname, Gender, DOB, Designation, and Mobile Number.
1. We can Update and View the My Account.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|User|[gs0004-users]({{< ref "gs0004-users" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_user_account_update|To update the user account|
|uc_user_account_view|To view the user account |


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|firstName|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "fname", length = 64, nullable = false)|fname varchar(64) NOT NULL|NO|YES|NO|YES|NO|NO||
|lastName|YES|NA|a-zA-Z0-9. _-, minlen=1, maxlen=32|@Column(name = "lname", length = 64, nullable = false)|lname varchar(64) NOT NULL|NO|YES|NO|YES|NO|NO||
|fsName|YES|NA|NA|@Column(name = "fsname", length = 64, nullable = false)|fsname varchar(64) NOT NULL|NO|YES|NO|YES|NO|NO||
|designation|YES|NA|NA|@Column(name = "designation", length = 24, nullable = false)|designation varchar(24) NOT NULL|NO|YES|NO|YES|NO|NO||
|gender|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "gender", length = 6, nullable = false)|gender varchar(6) NOT NULL|NO|YES|NO|YES|NO|NO||
|dob|YES|NA|Date Time|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP)	@Column(name = "dob", nullable = false)|dob datetime NOT NULL|NO|YES|NO|YES|NO|NO||
|mobileNumber|YES|NA|0-9|@Column(name = "mobile_number", length = 14, nullable = false)|mobile_number varchar(14) NOT NULL|NO|YES|NO|YES|NO|NO||

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
1. View page based on the standard UX Listing Template

### View Page Buttons
{{<mermaid align="left">}}
graph LR 
    UpdateBtn[Update]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	MyAccountMenu((My Account Menu))
	UpdatePage((Update Page))
    ViewPage((View Page))
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->MyAccountMenu
	MyAccountMenu-->ErrorPage
	ViewPage--U-->UpdatePage
	UpdatePage--SB-->ViewPage
	UpdatePage--SB-->UpdatePage
	MyAccountMenu--V-->ViewPage
	ErrorPage-->Stop
    %%For success Representation
    linkStyle 2 stroke:green,stroke-width:2px;
    linkStyle 3 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 1 stroke:red,stroke-width:2px;
    linkStyle 4 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|U|Update|
|V|View|
|F|Failure|
|SB|Submit or Back|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant MyAccountMenu as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        MyAccountMenu->>+Net: Check Internet, GET /app/User/account/view ViewPage
        Net--x-MyAccountMenu: F : Connection Error
        MyAccountMenu->>+cloud: S : GET /app/User/account/view ViewPage
        cloud-->>-MyAccountMenu: RES: MyAccount View
    end
    rect rgb(244,244,244)
        MyAccountMenu->>+Net: Check Internet, GET /app/User/account/update/form UpdateFormPage
        Net--x-MyAccountMenu: F : Connection Error
        MyAccountMenu->>+cloud: S : GET /app/User/account/update/form UpdateFormPage
        cloud-->>-MyAccountMenu: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        MyAccountMenu->>+Net: Check Internet, POST /app/User/account/update update
        Net--x-MyAccountMenu: F : Connection Error
        MyAccountMenu->>+cloud: S : POST /app/User/account/update Update
        cloud-->>-MyAccountMenu: RES: My Account Successfully Updated
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Update |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_201 **Negative Test Cases:** ut_n_u_GSTS_WEB_USERACCOUNT_200 ut_n_u_GSTS_WEB_USERACCOUNT_202|**Positive Test Cases:** Updating User with Authorised User **Negative Test Cases:**1.Updating User with Invalid Inputs 2.Updating User without DB Connection|  **firstName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **lastName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=1 and length<=64 3.null **fsName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null**gender** **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **designation:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **dob** |4|5|9|testAuthorisedUserUpdateUserAccount, testAuthorisedUserUpdateUserAccountWithoutDBConnection, testAuthorisedUserUpdateUserAccountNegativeTestCases|
|1.0| View |**Negative Test Cases:** ut_n_v_GSTS_WEB_USERACCOUNT_604 |**Negative Test Cases:** 1.Open User Account view without DB Connection| N/A |1|0|1|testAuthorisedUserAccountViewWithouDBConnection|
|1.0| Update Form |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_609 **Negative Test Cases:** ut_n_u_GSTS_WEB_USERACCOUNT_610 |**Positive Test Cases:** 1.Open User Account Update Form with Authorised User **Negative Test Cases:** 1.Open User Account Update Form without DB Connection| N/A |1|1|2|testAuthorisedUserOpenUserAccountUpdateForm, testAuthorisedUserOpenUserAccountUpdateFormWithoutDBConnection|

#### UnAuthorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Update |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_3 |Unauthorised User does not have permission to UPDATE|  **firstName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **lastName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=1 and length<=64 3.null **fsName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null**gender** **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **designation:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **dob** |1|N/A|1|testUnAuthorisedUserUpdateUserAccount| 

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the My Account should be provided in the User Manual.

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




 
