---
title: Change Password
tags : ["Composing"]
---

## Introduction
Change Password is one of the features of the software product. Change Password feature will provide the option to change the login password of the user.

## Business Assumptions
Change Password Feature should be planned at the design phase and updates to the password at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Change Password feature is accessible at all levels of organization.
1. New Password should not match with the last password.
1. New Password and Confirm Password should match to change the password.

### Non-functional Requirements
1. Current Password should be required to change the password.

### Problem Statement
1. Change Password feature is required to Change the login password of the user.

### Design 
1. Each Change Password has  Current Password, New Password, and Confirm Password.	
1. We can Change password always basis on the requirement.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|User|[gs0004-users]({{< ref "gs0004-users" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_change_password_reset|To reset the password|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Reset|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|----|
|currentPassword|YES|NA|NA|@Column(name = "login_password", length = 128, nullable = false)|login_password varchar(128) NOT NULL|NO|NO|YES|NO|NO|NO||
|loginPassword|YES|NA|NA|@Column(name = "login_password", length = 128, nullable = false)|login_password varchar(128) NOT NULL|NO|NO|YES|NO|NO|NO||
|confirmLogin Password|YES|NA|NA|@Column(name = "login_password", length = 128, nullable = false)|login_password varchar(128) NOT NULL|NO|NO|YES|NO|NO|NO||

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
1. Reset page based on the standard UX Listing Template

### List Page Buttons



### State Machine
{{<mermaid align="left">}}
flowchart TD
	ChangePasswordMenu((Change Password Menu))
	ResetPage((Reset Page))
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->ChangePasswordMenu
	ChangePasswordMenu-->ErrorPage
	ChangePasswordMenu--R-->ResetPage
	ResetPage--SB-->ResetPage
	ErrorPage-->Stop
    %%For success Representation
    linkStyle 2 stroke:green,stroke-width:2px;
    linkStyle 3 stroke:#cc33ff,stroke-width:2px;
    %%For failure representation
    linkStyle 1 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|R|Reset|
|U|Update|
|V|View|
|F|Failure|
|SB|Submit or Back|
|Green Arrow|Success|
|Red Arrow|Failure|
|Pink Arrow|Success or Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant ChangePasswordMenu as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        ChangePasswordMenu->>+Net: Check Internet, GET /app/User/resetPassword/form ResetFormPage
        Net--x-ChangePasswordMenu: F : Connection Error
        ChangePasswordMenu->>+cloud: S : GET /app/User/resetPassword/form ResetFormPage
        cloud-->>-ChangePasswordMenu: RES: Reset Form Loaded
    end
    rect rgb(244,244,244)
        ChangePasswordMenu->>+Net: Check Internet, POST /app/User/resetPassword Reset
        Net--x-ChangePasswordMenu: F : Connection Error
        ChangePasswordMenu->>+cloud: S : POST /app/User/resetPassword Reset
        cloud-->>-ChangePasswordMenu: RES: Password Reset Successful
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------| 
|1.0| Reset |**Positive Test Cases:** ut_p_c_GSTS_WEB_USERACCOUNT_301 **Negative Test Cases:** ut_n_c_GSTS_WEB_USERACCOUNT_300 ut_n_c_GSTS_WEB_USERACCOUNT_302|**Positive Test Cases:** Reset the User login password with Authorised User **Negative Test Cases:** 1.Reset the User login password with Invalid Input 2.Reset the User login password without DB Connection|  **currentPassword:** 1.valid characters 2. length>=7 and length<=128 3.null **loginPassword:** 1.valid characters 2. length>=7 and length<=128 **confirmLoginPassword:** 1.valid characters 2. length>=7 and length<=128|5|3|8|testAuthorisedUserResetPasswdWithoutDBConnection, testAuthorisedUserResetPasswd, testAuthorisedUserResetPasswdNegativeTestcase|
|1.0| Forgot Password Form |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_600 |**Positive Test Cases:** Open User Forgot Password Form with Authorised User | N/A|1|0|1|testAuthorisedUserOpenForgotPasswordForm|
|1.0| Forgot Password Update Form |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_611 |**Positive Test Cases:** Get User Forgot Password update Form with Authorised User | N/A|1|0|1|testAuthorisedUserUserForgotPasswordUpdateForm|
|1.0| Forgot Password Update |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_624 **Negative Test Cases:** ut_n_u_GSTS_WEB_USERACCOUNT_619 ut_n_u_GSTS_WEB_USERACCOUNT_620 ut_n_u_GSTS_WEB_USERACCOUNT_621 ut_n_u_GSTS_WEB_USERACCOUNT_622 ut_n_u_GSTS_WEB_USERACCOUNT_623 |**Positive Test Cases:** 1.Get User Forgot Password Update with Authorised User **Negative Test Cases:** 1.Get User Forgot Password Update with Empty Random Token 2.Get User Forgot Password Update with Invalid Random Token 3.Get User Forgot Password Update with Invalid Password 4.Get User Forgot Password Update with Invalid Username 5.Get User Forgot Password Update without DB Connection| N/A|1|5|6|testAuthorisedUserUserForgotPasswordUpdate, testAuthorisedUserUserForgotPasswordUpdateWithEmptyRandomToken, testAuthorisedUserUserForgotPasswordUpdateWithInvalidRandomToken, testAuthorisedUserUserForgotPasswordUpdateWithInvalidPassword, testAuthorisedUserUserForgotPasswordUpdateWithInvalidUserName, testAuthorisedUserUserForgotPasswordUpdateWithoutDBConnection|
|1.0| Forgot Password Otp |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_614 **Negative Test Cases:** ut_n_u_GSTS_WEB_USERACCOUNT_615 ut_n_u_GSTS_WEB_USERACCOUNT_616 ut_n_u_GSTS_WEB_USERACCOUNT_617 ut_n_u_GSTS_WEB_USERACCOUNT_618 |**Positive Test Cases:** Get User Forgot Password Otp with Authorised User **Negative Test Cases:** 1.Get User Forgot Password Otp with Invalid Username 2.Get User Forgot Password Otp with Empty UserName 3.Get User Forgot Password Otp without DB Connection 4.Get User Forgot Password Otp with Empty Random Token| 1.Username|1|3|4|testAuthorisedUserUserForgotPasswordOtp, testAuthorisedUserUserForgotPasswordOtpWithInvalidUserName, testAuthorisedUserUserForgotPasswordOtpWithEmptyUserName, testAuthorisedUserUserForgotPasswordOtpWithoutDBConnection, testAuthorisedUserUserForgotPasswordOtpWithEmptyRandomToken|
|1.0| Reset Password Form |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_601 |**Positive Test Cases:** Open User Reset Password Form with Authorised User | N/A|1|0|1|testAuthorisedUserOpenResetPasswordForm|
|1.0| Reset Password Update Form |**Positive Test Cases:** ut_p_u_GSTS_WEB_USERACCOUNT_612 |**Positive Test Cases:** Get User Forgot Password Reset Form with Authorised User | N/A|1|0|1|testAuthorisedUserUserForgotPasswordReset|

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




 
