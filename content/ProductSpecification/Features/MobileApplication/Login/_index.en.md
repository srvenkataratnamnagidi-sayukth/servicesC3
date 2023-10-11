---
title: Login
tags : ["Composing"]
---

## Introduction
Login is one of the basic features of the software product which contains confidential data. The product can be used by different users at various levels of the organization. 
To access the application, every user should authenticate. The login page allows a user to gain access to an application by entering their username and password.

## Business Assumptions
1. Login feature should be planned at the design phase.
1. Only authorized users can be logged in to the application.
1. Authentication type is **"username and password"**.
1. Before using the sign-in feature user should sign up in the application.

## Requirements
### Functional Requirements
1. Required a valid Username. Username is an email.
1. Required a password. Password should maintain format. The format is **a minimum of eight characters, at least one uppercase letter, one lowercase letter, one number, and one special character**.

### Non-functional Requirements
1. Using the same credentials user can log in to one or more devices. 

    Explanation : The user logged in one mobile it facing some issues. The user can able to sign in another mobile device using the same credentials and continue his/her survey.

### Problem Statement
The login feature is required to access the application, only authorized users can be logged in to the application.

### Design 
1. Login Feature contains Username, Password fields and Sign In button.
1. After entering a valid username, password and click on the sign-in button result the user to Dashboard page.
1. Username field is set to default with a username value, if the user previously logged in to the application.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Sign Up|-|You can only use the login feature when you first sign up for the application.|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_login|To log in to the application.|
|uc_offline_login|To log in to the application in offline mode. If login time less than 7 days, then only offline login work.|
|uc_set_default_login_name|Username field is set to default with a username value, if the user previously logged in to the application.|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set Layout/API|SQLite Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|
|id|YES|NA|a-zA-Z0-9,@#&_()-., maxlen=128|id String|NA|NA|NA|NO|NO|NO||
|loginName|YES|NA|a-zA-Z0-9,@#&_()-., maxlen=50|loginName String|NA|NA|NA|NO|NO|NO||
|password|YES|NA|a-zA-Z0-9_.@$!%&, maxlen=50|password String|NA|NA|NA|NO|NO|NO||
|loginTime|YES|NA|a-zA-Z0-9, maxlen=128|loginTime String|NA|NA|NA|NO|NO|NO||
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
|userId|YES|NA|a-zA-Z0-9, maxlen=128|userId String|NA|NA|NA|NO|NO|NO||
|userName|YES|NA|a-zA-Z0-9, maxlen=128|userName String|NA|NA|NA|NO|NO|NO||
|designation|YES|NA|a-zA-Z0-9, maxlen=128|designation String|NA|NA|NA|NO|NO|NO||
|profileImage|YES|NA|a-zA-Z0-9, maxlen=128|profileImage String|NA|NA|NA|NO|NO|NO||
|flushData|YES|NA|a-zA-Z0-9, maxlen=128|flushData Boolean|NA|NA|NA|NO|NO|NO||


#### Feature Permission
No feature permission for this login feature.

|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|

## Acceptance Criteria
||
|--|
|1. Anyone who has this application can view the sign-in feature. But the authorized user can only log in to the application.|
|2. Offline login is also accepted if login time less than seven days.

## User Experience
### Login Feature
{{<mermaid align="left">}}
graph LR 
    SignInBtn[Sign in]
{{< /mermaid >}}





### state machine
{{<mermaid align="center">}}
flowchart TD
    SignInPage(( Sign in Page))
	SignInBtn[Sign in Button]
	DashboardPage[Dashboard Page]
	SignInPage--C-->SignInBtn
	linkStyle 0 stroke:blue,stroke-width:2px,color:black;
	SignInBtn--S-->DashboardPage
	linkStyle 1 stroke:green,stroke-width:2px,color:black;
	SignInBtn--F-->SignInPage 
	linkStyle 2 stroke:red,stroke-width:2px,color:black;
{{< /mermaid >}}

| Symbol| Description|
|--|--|
| C| OnClick|
| S| OnSuccess|
| F| OnFailure|


### User Login flow : offline and online
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%

flowchart TD
    start((start))
    checkInputFields{Input Fields Empty or Invalid}
    showMessage>Message : Invalid or Empty Username / Password]
    loadAllUsers[Load All Users]
    userExistenceInLocalDB{User Not Null}
    usersCountInLocalDB{Users Count > 0 }
    loadSingleUserWithName[Load User With Provided Username]
    invokeLoginAPI{AuthenticateUser API Call}
    checkNetworkConnection{Internet Connection}
    showMessageNetworkConnection>Message : Please Connect With Internet]
    showMessageUnauthorized>Message : Unauthorized, Invalid Username / Password]
    validateDBLogin{User Login >= 7 days}
    invokeContext{GetContext API Call}
    showMessageApiError>Show Message :API Error message]
    invokeUserSession{GetUserSession API Call}
    showDashboard[Dashboard]
    End((end))
    start--Input : Username & Password-->checkInputFields
    checkInputFields--true-->showMessage
    checkInputFields--false-->loadAllUsers
    loadAllUsers-->usersCountInLocalDB
    usersCountInLocalDB--true-->loadSingleUserWithName
    loadSingleUserWithName-->userExistenceInLocalDB
    userExistenceInLocalDB--true-->validateDBLogin
    userExistenceInLocalDB--false-->checkNetworkConnection
    checkNetworkConnection--false-->showMessageNetworkConnection
    checkNetworkConnection--true-->invokeLoginAPI
    usersCountInLocalDB--false-->checkNetworkConnection
    invokeLoginAPI--response != 200-->showMessageUnauthorized
    invokeLoginAPI--response == 200-->invokeContext
    validateDBLogin--false-->showDashboard
    validateDBLogin--true-->checkNetworkConnection
    invokeContext--response == 200--> invokeUserSession
    invokeContext--response != 200--> showMessageApiError
    invokeUserSession--response == 200--> showDashboard
    invokeUserSession--response != 200--> showMessageApiError
    showDashboard-->End
{{< /mermaid >}}

### Login Module & GS-Cloud Operations :
#### [Routing API](http://localhost:1313/productspecification/features/mobileapplication/api/routing-api/)

{{<mermaid align="center">}}
sequenceDiagram
	participant Dashboard as Dashboard
	participant SQLite as SQLite Database
    participant Login as Login Module
    participant Net as Network Utils
    participant cloud as GS-Cloud
    autonumber
   
    rect rgb(244,244,244)
        Login->>+SQLite: get RouteHostname
        SQLite-->>-Login: RouteData Object
        Note right of Login: If RouteData == NULL { refer Routing API  } else { go to step ( 3 ) }
    end

    rect rgb(244,244,244)
        Login->>+SQLite: Load All Users
        SQLite-->>-Login: List of Users

        Note right of Login: If UserSize > 0
        Login->>+SQLite: Load User with given Username
        SQLite-->>-Login: User Object
    end

    rect rgb(244,244,244)
        Note right of Login: If Hostname ! = NULL
        Note right of Login: If User Size less than 0 ( or ) User object null ( or )  User login time greater than 7 days.
        Login->>+Net: Check Internet , InvokeAuthApi
        Net--x-Login: F : Connection Error
        Login->>+cloud: S : POST "https://{hostname}/api/login" login
        cloud-->>-Login: RES 200
    end

    rect rgb(244,244,244)
        Login->>+Net: Check Internet , GetContext
        Net--x-Login: F : Connection Error
        Login->>+cloud: S : GET "https://{hostname}/api/{apiVer}/CtxDto" getContext
        cloud-->>-Login: RES 200
    end

    rect rgb(244,244,244)
        Login->>+Net: Check Internet , GetUserSession
        Net--x-Login: F : Connection Error
        Login->>+cloud: S : "GET https://{hostname}/api/{apiVer}/user/{userId}" getUserSession
        cloud-->>-Login: RES 200
    end

    rect rgb(244,244,244)
        Note right of Login: If Response == 200
        Login->>+SQLite: insert or update Login user
    end

    rect rgb(244,244,244)
        Login->>Dashboard: Auth Success
    end

{{< /mermaid >}}


[comment]: <> (### Request and Response JSON Data: based on operation number)

[comment]: <> (#### **Payload RouteData Object :**)

[comment]: <> (Route Data Object From Local Database)

[comment]: <> (        {)

[comment]: <> (            "expiryTime":1608196803034,)

[comment]: <> (            "hostnameApd":"ts.gramsevak.gov9.in",)

[comment]: <> (            "hostnameApi":"ts.gramsevak.gov9.in",)

[comment]: <> (            "hostnameApp":"ts.gramsevak.gov9.in",)

[comment]: <> (            "id":"4ff26169-7ed5-4064-a1ad-71eeea676168",)

[comment]: <> (            "state":"qats",)

[comment]: <> (            "surveyCompanyList":"[ Shadkona Tech Pvt Ltd, ApptoneLabs Tech Pvt Ltd ]")

[comment]: <> (        })

        

[comment]: <> (#### **Payload POST /api/invokeRouteAuth invokeRouteAuthentication :**)

[comment]: <> (Request sent : Anonymous user          )
        
[comment]: <> (        {)

[comment]: <> (            "password":"39ae086a-8cab-40b5-93ef-7ec6905b6aa4",)

[comment]: <> (            "username":"39ae086a-8cab-40b5-93ef-7ec6905b6aa4#@@#ebSCwqhJrSxF5z/ZYGEVKdo3WIw2uYCDsxXucSDzCD76ZVMcgsz/oqpw1RK3YAIfrQQ4vnFOIMDykpKqOivbvA==")

[comment]: <> (        })
       
[comment]: <> (Response: authToken   )
        
[comment]: <> (        authToken : Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6I)

[comment]: <> (                    jM4MTQ4NDIxLWFmZGItNDMwNy1hYTA1LTExN2QzMTJkN2RlZiIsImV4cCI6MTYwODQ1NjAwMSwicm9sIjpbIlJPTEVfQURNSU4iLCJST0x)

[comment]: <> (                    FX1NDT1BFX1NUQVRFIl19.c71kaQUeaeGURnS5YB-M6EAwo51UsyPjVWMedCBUdAQgI7ep-4TTeOco7A-wFx4Iu83sl4a2fJI3rvIcoOeVqg)
        
        
[comment]: <> (#### **Payload GET /api/1/Route/qats getStagingHostname :**)

[comment]: <> (Response :)
        
[comment]: <> (        {)

[comment]: <> (            "state":"qats",)

[comment]: <> (            "hostnameMap":{ )

[comment]: <> (                            "app":"ts.gramsevak.gov9.in",)

[comment]: <> (                            "apd":"ts.gramsevak.gov9.in",)

[comment]: <> (                            "api":"ts.gramsevak.gov9.in")

[comment]: <> (                          },)

[comment]: <> (            "surveyCompanyList":["Shadkona Tech Pvt Ltd","ApptoneLabs Tech Pvt Ltd"],)

[comment]: <> (            "expiryTime":1608198685842})

[comment]: <> (#### **Payload persistInLocalDB&#40;RouteData routeData&#41; :**)

[comment]: <> (Insert or Update Route Data object in Local Database)

[comment]: <> (    {"state":"qats","hostnameMap":{"app":"ts.gramsevak.gov9.in","apd":"ts.gramsevak.gov9.in","api":"ts.gramsevak.gov9.in"},"surveyCompanyList":["Shadkona Tech Pvt Ltd","ApptoneLabs Tech Pvt Ltd"],"expiryTime":1608198685842})




[comment]: <> (#### **Payload Load All Login Users :**)

[comment]: <> (All Login Users From Database)

[comment]: <> (        [)

[comment]: <> (            {   )

[comment]: <> (                "designation":"Survey Executive",)

[comment]: <> (                "flushData":true,)

[comment]: <> (                "id":"0a4e0946-36e5-48d7-be49-75014a9b9484",)

[comment]: <> (                "loginName":"nagasai.cs14@gmail.com",)

[comment]: <> (                "loginTime":"12/03/2020 13:08:56",)

[comment]: <> (                "offlineTimeout":604800000,)

[comment]: <> (                "password":"nagasai234@Shadkona",)

[comment]: <> (                "profileImage":"iVBORw0KGgoAA)

[comment]: <> (            })

[comment]: <> (        ])

[comment]: <> (#### **Payload Fetching User Based on Given Username.**)

[comment]: <> (Current Login User From Database)

[comment]: <> (        {)

[comment]: <> (            "designation":"Survey Executive",)

[comment]: <> (            "flushData":true,)

[comment]: <> (            "id":"0a4e0946-36e5-48d7-be49-75014a9b9484",)

[comment]: <> (            "loginName":"nagasai.cs14@gmail.com",)

[comment]: <> (            "loginTime":"12/03/2020 13:08:56",)

[comment]: <> (            "offlineTimeout":604800000,)

[comment]: <> (            "password":"nagasai234@Shadkona",)

[comment]: <> (            "profileImage":"iVBORw0KGgoAA)

[comment]: <> (        })
 
[comment]: <> (####  **Payload POST /api/auth Authentication**)

[comment]: <> (Request : )

[comment]: <> (**Method** : POST)

[comment]: <> (**Headers** : )

[comment]: <> (+ **Accept**:application/json)

[comment]: <> (+ **Content-type**:application/json)


[comment]: <> (**Request body**  :   )
            
[comment]: <> (    {)

[comment]: <> (        "password": "1!Qdesigner",)

[comment]: <> (        "username": "admin@local.com")

[comment]: <> (        "version": "1",)

[comment]: <> (        "devUuid":"Device UUID value")

[comment]: <> (    })
            
            
[comment]: <> (Response:)
  
[comment]: <> (  200 OK)
  
[comment]: <> (**Response Header**)

[comment]: <> (+ **authorization** : Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ)


[comment]: <> (####  **payload GET /api/getContext GetContext**)

[comment]: <> (**Method** : GET)

[comment]: <> (**Headers**  : )

[comment]: <> (+ **Accept**: application/json)

[comment]: <> (+ **Content-Type**: application/json)

[comment]: <> (+ **Authorization**: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ)

[comment]: <> (**Request body**: -)

[comment]: <> (**Response Status**: 200 OK)

[comment]: <> (**Response**: )

[comment]: <> (    {)

[comment]: <> (        "stateId": "3f06af63-a93c-11e4-9797-005056907001",)

[comment]: <> (        "distId": "3f06af63-a93c-11e4-9797-005056907102",)

[comment]: <> (        "divId": "3f06af63-a93c-11e4-9797-005056907110",)

[comment]: <> (        "mandalId": "3f06af63-a93c-11e4-9797-005056907114",)

[comment]: <> (        "panchayatId": "3f06af63-a93c-11e4-9797-005056907115",)

[comment]: <> (        "stateName": "Andhra Pradesh",)

[comment]: <> (        "distName": "West Godavari",)

[comment]: <> (        "divName": "Narsapuram",)

[comment]: <> (        "mandalName": "Bhimavaram",)

[comment]: <> (        "panchayatName": "Kalipatnam",)

[comment]: <> (        "docUrl":"http://doc.ts.gramsevak.telangana.gov9.in",)

[comment]: <> (        "videoUrl":"www.youtube.com/channel/UCQqCWfCwR-zo21w6N0Mb_sQ",)

[comment]: <> (        "supportLine01":"+91 8019016661",)

[comment]: <> (        "supportLine02":"+91 8019016662",)

[comment]: <> (        "supportLine03":"+91 8019016663")

[comment]: <> (    })
    
    
[comment]: <> (#### **Payload GET /api/getUserSession GetUserSession**)

[comment]: <> (**Method** : GET)

[comment]: <> (**Headers**  : )

[comment]: <> (+ **Accept**: application/json)

[comment]: <> (+ **Content-Type**: application/json)

[comment]: <> (+ **Authorization**: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ)

[comment]: <> (**Request body** : -)

[comment]: <> (**Response Status** : 200 OK)

[comment]: <> (**Response** : )

[comment]: <> (    {)

[comment]: <> (        "sessionTimeout": 3600000,)

[comment]: <> (        "offlineTimeout": 604800000,)

[comment]: <> (        "userId": "1a58bb06-4f72-4353-bf02-cfb33eec454c",)

[comment]: <> (        "userName": "Nagidi Nagidi",)

[comment]: <> (        "designation": "Panchayat Secretary",)

[comment]: <> (        "flushData": true)
        
[comment]: <> (    })
 
[comment]: <> (#### **Payload insert or update Login user :**)

[comment]: <> (Inserting Login user Data in Database)

[comment]: <> (    {)

[comment]: <> (        "designation":"Survey Executive",)

[comment]: <> (        "flushData":true,)

[comment]: <> (        "id":"a48bd24a-a4c4-4529-9111-58fa05401122",)

[comment]: <> (        "loginName":"nagasai.cs14@gmail.com",)

[comment]: <> (        "loginTime":"12/10/2020 16:07:03",)

[comment]: <> (        "offlineTimeout":604800000,)

[comment]: <> (        "password":"nagasai234@Shadkona",)

[comment]: <> (        "profileImage":"iVBORw0KGgoAAAANS")

[comment]: <> (    })


## Security compliance check
1. Only user having the credentials should logged in to application

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1.

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







 



 
