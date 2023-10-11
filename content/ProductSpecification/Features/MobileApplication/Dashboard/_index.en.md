---
title: Dashboard
tags : ["Composing"]
---

## Introduction
Dashboard is the building block of the Application.It is divided into three segments namely **Survey Summary** , **Survey Performance** 
and **Current Survey Summary**
**Survey Summary**:- This holds the information about the data.That is how much survey is completed Today,Yesterday ,This week ,
                     This Month and This Projects.
**Survey Performance** :- It contains the information about Total Panchayats,Average Survey Time and Updated time.
**Current Survey Summary**:- It contains the information about modules created and average time taken to create those modules.                   

## Business Assumptions
1.Dashboard feature should be planned at design phase.
2. Only authorized users can view the Dashboard Page.

## Requirements
### Functional Requirements
1. Dashboard page should divide into Three segments namely Survey Summary, Survey Performance and Current Survey Summary.
1. Whenever survey executive updated any details in the application it should updated in the Dashboard module.
1. Average survey time should calculate for every module and should represent in Dashboard page. 


### Non-functional Requirements
1. Using multiple devices user can view Dashboard with same Login Credentials.

### Problem Statement
Dashboard page is building block of the application because it shows us the performance of the App as well as survey executive.   

### Design 
1. Dashboard Tag should present at the top of the Module
1. Page should divide into three segment namely Survey Summary , Survey Performance and Current Survey Summary
1. Survey Summary holds the data about survey with reference of time like what it is today,yesterday and from one month.
1. Survey Perfomance holds data about panchayaths and average survey time and last updated time.
1. Current Survey Summary holds the data about Each property in the Application.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|LogIn|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_view_Dashboard|To view the Survey Summary Details|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|TodayAssetCount|YES|NA|a-zA-Z0-9, maxlen=128|todayAssetCount String|NA|NA|NA|NA||
|YesterdayAssetCount|YES|NA|a-zA-Z0-9, maxlen=128|yesterdayAssetCount String|NA|NA|NA|NA|NA|NA||
|WeekAssetCount|YES|NA|a-zA-Z0-9, maxlen=128|weekAssetCount String|NA|NA|NA|NA|NA|NA||
|ThisMonth|YES|NA|a-zA-Z0-9, maxlen=128|thisMonth String|NA|NA|NA|NA|NA|NA||
|TotalAssetCount|YES|NA|a-zA-Z0-9, maxlen=128|totalAssetCount String|NA|NA|NA|YES|YES|NO||
|TotalPanchayatCount|YES|NA|a-zA-Z0-9, maxlen=128|toatlPanchayatCount String|NA|NA|NA|YES|YES|NO||
|AverageAssetTime|YES|NA|a-zA-Z0-9, maxlen=128|averageAssetTime String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatAssetCount|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatAssetCount String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatKolagaramCount|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatKolagaramCount String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatAdvertisementCount|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatAdvCount String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatTradeLicenceCount|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatTradeCount String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatAuctionCount|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatAuctionCount String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatVacantLandCount|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatVacantCount String|NA|NA|NA|YES|YES|NO||
|UpdateTime|YES|NA|a-zA-Z0-9, maxlen=128|updateTime String|NA|NA|NA|YES|YES|NO||
|ErrorMultipleOrg|YES|NA|a-zA-Z0-9, maxlen=128|errorMultuple String|NA|NA|NA|YES|YES|NO||
|CurrentPanchayatId|YES|NA|a-zA-Z0-9, maxlen=128|currentPanchayatId String|NA|NA|NA|YES|YES|NO||
|PanchayatName|YES|NA|a-zA-Z0-9, maxlen=128|panchayatName String|NA|NA|NA|YES|YES|NO||
|MandalName|YES|NA|a-zA-Z0-9, maxlen=128|mandalName String|NA|NA|NA|YES|YES|NO||
|DivisionName|YES|NA|a-zA-Z0-9, maxlen=128|divisionName String|NA|NA|NA|YES|YES|NO||
|DistrictName|YES|NA|a-zA-Z0-9, maxlen=128|districtName String|NA|NA|NA|YES|YES|NO||
|StateName|YES|NA|a-zA-Z0-9, maxlen=128|stateName String|NA|NA|NA|YES|YES|NO||
|LandSurveyNumbers|YES|NA|a-zA-Z0-9, maxlen=128|landSurveyNumber String||NA|NA|NA|YES|YES|NO||


#### Feature Permission

| Permission code | Action |
|-----------------|--------|
| -               | -      |
| -               | -      |

## Acceptance Criteria
1. All Users who are authorized can view and access the Dashboard Module.

## User Experience

### Flow of the dashboard 

{{<mermaid align="center">}}
graph TD
	start((Start))
	apiCall{API call:getDashboard}
	supportApi[call Support Api]
	response{Response}
	getSupport[getSupportDto]
	alert>Show Alert]
	failedToken{Failed Token}
	unSuccess{==UNSUCCESS}
	gotoLogin[Navigate to Login Page]
	apiforLogin{Api for Login}
	getContext[get Context]
	getDashboard[get Dashboard Details]
	showAlert>Alert Message]
	End((end))
	start-->apiCall
	subgraph API
		apiCall--==200-->supportApi
		apiCall--==400-->showAlert
		supportApi-->response
		response--==200-->getSupport
		getSupport-->getDashboard
		response--==401-->alert
	end
	getDashboard-->End
	alert-->End
	subgraph tokenfailed
		apiCall--==401-->failedToken
		failedToken--NotNull-->unSuccess
		unSuccess--true-->gotoLogin
		failedToken--Null-->apiforLogin
		apiforLogin--==200-->getContext
		getContext-->supportApi
	end
	gotoLogin-->End	
	
{{< /mermaid >}}

### Sequence of actions in Dashboard module
{{<mermaid align="center">}}
sequenceDiagram
	participant M as Mobile
	participant SQL as SQLite
	participant KV as KV-DB
	participant Net as Network Utils
	participant S as GS-Cloud 
	autonumber
	M->>Net: Check Network, POST/api/1/getDashboard();
	Net-->>M: F:Connection Error
	M->>S: S:POST/api/1/getDashboard();
	S-->>M: RES:200
	M->>Net: Check Network, POST/api/1/getSupportData();
	Net-->>M: F:Connection Error(Show Alert Message)
	M->>S: S:POST/api/1/getSupportData();
	S-->>KV: RES:200 saveSupportData & saveDashboardData();
	S-->>M: F:401 gotoLoginPage
	S-->>M: F:400 Show Alert
	
	
{{</mermaid>}}


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




 
