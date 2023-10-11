---
title: Side Menu
tags : ["Composing"]
---

## Introduction
Side Menu is the one of the feature in the application.By using side menu User can go to all other modules in the application.Other modules that are navigate from Side Menu are Dashboard,Start/Continue Survey,Panchayat,Upload Data ,Complete Survey ,User Manual , Customer Care , About and Lagout .
**Dashboard**:- Dashboard contains the information about entire survey i.e., Survey Count, Survey Performance and Current Survey Count.
**Survey**:- To start or continue survey of House,Auction,Advertisement,TradeLicense,Kolagaram,Locked Property and Vacant Land.   
**Panchayat**:- To select panchayat in order to start the survey. 
**Upload Data**:-To sync the data that collected from the Citizens in the panchayat.
**Complete Survey**:-After data got successfully uploaded we have to complete survey to understand all the modules in the selected panchayat were completed.
**User Manual**:- To guide the User/Survey Executive about the product.
**Customer Care**:-If User get any doubt about product to give clarity on that we have customer care.
**About**:-About provides information the application.
**Logout**:- When survey executive click on Logout he we redirect to Login Screen. 

## Business Assumptions
1. Only authorized users can view the Dashboard
2. After LogIn successfully then only user can view the Dashboard
## Requirements
### Functional Requirements
1. Only authorized users can view the Dashbord page.
1. Survey Executive Name and Image should be same as the details that given when Sign Up.
1. User has to view all the modules in the Dashboard Fragment i.e Dashboard,Start/Continue Survey,Panchayat,Upload Data ,Complete Survey ,User Manual , Customer Care , About and Lagout .
1. User should redirect to the segment that he/she Clicked On.

### Non-functional Requirements
1.Survey Executive can access Dashboard from multiple divices.

### Problem Statement
1. Dashboard is the basic building block of the Application.
      Explanation : From the Dashboard module only Survey Executive Or Application Users able to go to any module from this Dashboard page Only. 


### Design 
1. After Login got successful user can view the Side Menu. 
1. To the left side of the page we should have Side Menu.
1. Application user Photo and Designation should come at top of the Side Menu.
 

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|DashBoard |[GS0003-Login]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_view_sideMenu|To view the data that appears in Dashboard page.|


#### Model Attributes
| Attribute name | Mandatory | Default value | Input Allowed Char set JSP/API | HSQL Column Definition                                                     | SQL Column Definition           | Create | Update | Remove | View | List | Search | Remarks |
|----------------|-----------|---------------|--------------------------------|----------------------------------------------------------------------------|---------------------------------|--------|--------|--------|------|------|--------|---------|
| name           | YES       | NA            | a-zA-Z0-9, maxlen=64           | @Column(name = "name", length = 64, unique = true, nullable = false)       | name varchar(64) not null       | NA     | NA     | NA     | YES  | YES  | YES    ||
| code           | YES       | NA            | a-zA-Z0-9, maxlen=32           | @Column(name = "code", length = 32, unique = true, nullable = false)       | code varchar(32) not null       | NA     | NA     | NA     | YES  | YES  | NO     ||
| descr          | YES       | NA            | a-zA-Z0-9, maxlen=128          | @Column(name = "descr", length = 128, unique = true, nullable = false)     | descr varchar(128) not null     | NA     | NA     | NA     | NO   | YES  | YES    ||
| groupName      | YES       | NA            | a-zA-Z0-9, maxlen=32           | @Column(name = "group_name", length = 32, unique = true, nullable = false) | group_name varchar(32) not null | NA     | NA     | NA     | YES  | YES  | NO     ||

#### Feature Permission


| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |

## Acceptance Criteria
1. Anyone who sign-in to this Application can view the Dashboard page.

## User Experience
### Action Selection from Dashboard Side Menu
{{<mermaid align="left">}}
graph LR 
      DashboardBtn[  Dashboard ]
    StartSurveyBtn[Survey]
    PanchayatBtn[Panchayat]
    UploadBtn[Upload Data]
    completeSurveyBtn[Complete Survey]
    userManualBtn[User Manual]
    CustomerBtn[Customer Care]
    aboutBtn[About]
    logoutBtn[LogOut]
{{< /mermaid >}}

### State Machine

{{<mermaid align="left">}}
flowchart TD
	DashboardPage(( Dashboard ))
	StartSurveyBtn[Start Survey]
	PanchayatBtn[Panchayat]
	UploadBtn[Upload Data]
	CompleteSurveyBtn[Complete Survey]
	UserManualBtn[User Manual]
	CustomerBtn[Customer Care]
	AboutBtn[About]
	LogoutBtn[Logout]
	StartPage[Survey]
	PanchayatPage[Panchayat Page]
	UploadDataPage[Upload Data Page]
	CompleteSurveyPage[Complete Survey Page]
	UserManualPage[User Manual Page]
	CustomerCArePage[Customer Care Page]
	AboutPage[About Page]
	LogoutPage[Logout Page]
	subgraph Dashboard
	DashboardPage
	end
	subgraph Start/Continue Survey
	DashboardPage--C-->StartSurveyBtn
	StartSurveyBtn--F-->DashboardPage
	StartSurveyBtn--S-->StartPage
	end
	subgraph Panchay
	DashboardPage--C-->PanchayatBtn
    PanchayatBtn--F-->DashboardPage
	PanchayatBtn--S-->PanchayatPage
	end 
	subgraph Upload Data
	DashboardPage--C-->UploadBtn
	UploadBtn--F-->DashboardPage
	UploadBtn--S-->UploadDataPage
	end
	subgraph Complete Survey
	DashboardPage--C-->CompleteSurveyBtn	
	CompleteSurveyBtn--F-->DashboardPage
    CompleteSurveyBtn--S-->CompleteSurveyPage
    end 
    subgraph User Manual
    DashboardPage--C-->UserManualBtn
    UserManualBtn--F-->DashboardPage
    UserManualBtn--S-->UserManualPage
    end
    subgraph Customer Care
    DashboardPage--C-->CustomerBtn 
	CustomerBtn--F-->DashboardPage
	CustomerBtn--S-->CustomerCArePage
	end
	subgraph About
	DashboardPage--C-->AboutBtn
	AboutBtn--F-->DashboardPage
	AboutBtn--S-->AboutPage
	end
	subgraph Logout
	DashboardPage--C-->LogoutBtn
	LogoutBtn--F-->DashboardPage
    LogoutBtn--S-->LogoutPage
    end
    %%For success Representation
    linkStyle 2 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    linkStyle 17 stroke:green,stroke-width:2px;
    linkStyle 20 stroke:green,stroke-width:2px;
    linkStyle 23 stroke:green,stroke-width:2px;   
    %%For failure Representation
    linkStyle 1 stroke:red,stroke-width:2px;
    linkStyle 4 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
    linkStyle 19 stroke:red,stroke-width:2px;
    linkStyle 22 stroke:red,stroke-width:2px;
    %%For Onclick Representation
    linkStyle 0 stroke:blue,stroke-width:2px;
    linkStyle 3 stroke:blue,stroke-width:2px;
    linkStyle 6 stroke:blue,stroke-width:2px;
    linkStyle 9 stroke:blue,stroke-width:2px;
    linkStyle 12 stroke:blue,stroke-width:2px;
    linkStyle 15 stroke:blue,stroke-width:2px;
    linkStyle 18 stroke:blue,stroke-width:2px;
    linkStyle 21 stroke:blue,stroke-width:2px;
     
{{< /mermaid >}}


| Symbol| Description|Line Color Indication
|--|--|--|
| C| OnClick|Blue|
| S| OnSuccess|Green|
| F| OnFailure|Red|


### Flowchart for the Dashboard
{{<mermaid align="center">}}
flowchart TD
    start((start))
    Check{Clicked On}
    Start/continue[Start/Continue Surey Page]
    Panchayat[Panchayat Page]
    Upload[Upload Data Page]
    complete[Complete Survey Page]
    UserManual[User Manual Page]
    Customer[Customer Care Page]
    About[About Page]
    Logout[Logout Page]
    end1((end))
    start-->Check
    Check--Start/Continue Surey-->Start/continue
    Start/continue-->end1
    Check--Panchayat-->Panchayat
    Panchayat-->end1
    Check--Upload Data-->Upload
    Upload-->end1
    Check--Complete Survey-->complete
    complete-->end1
    Check--User Manual-->UserManual
    UserManual-->end1
    Check--Customer Care-->Customer
    Customer-->end1
    Check--About-->About
    About-->end1
    Check--Logout-->Logout
    Logout-->end1
   
{{< /mermaid >}}

## Security compliance check
1. Only user having the permission ROLE_PERMISSION_VIEW should view this functionality 

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
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

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




 
