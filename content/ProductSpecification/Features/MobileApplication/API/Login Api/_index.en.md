---
title: Login Api
tags : ["Composing"]
---

## API Call - URL Description
|API Call|Method|URL Endpoint|Description|
|-----------|--------|-------|-------------|
|login|POST|/api/login|To authenticate the user|
|getContext|GET|/api/1/CtxDto|To get the panchayat data ex: State, District, Division, Mandal, Panchayat etc..|
|getUserSession|GET|/api/1/UserSessionDto |To get the userSession ex: sessionTimeout, offlineTimeout,userId, username, designation. |

### Description :

1. Get the User from database. If the user is not null and valid user then navigate the user to Dashboard screen.
   - If the user is null then invoke the api call login ( https://{hostname}/api/login ).
2. If the response from api call login is 200 then save the response data ( Authorization, s-jwt-token, set-cookie) in PreferenceHelper preference , ContextPreference and invoke the api call getContext ( https://{hostname}/api/{apiVer}/CtxDto ).
   - If the response is other than 200 show error message
3. If the response from api call context is 200 then invoke the api call userSession ( https://{hostname}/api/{apiVer}/user/{userId} )
    - If the response is other than 200 show error message
4. If the response from api call userSession then get the response data, save the user session data in UserSessionPreference, prepare the User object and save it database.
    - If the response is other than 200 show error message




### 1.API call for login to the Mobile Application
 **URL Structure:**  https://{hostname}/api/login
 
 **URL:**  https://ts.gramsevak.net/api/login
 
 **Method** : POST
 
 #### Headers : 
 
 >**Accept:** application/json  
 **Content-type:** application/json
 
 #### Request body  :
 
    {
        "password":"xxxxxxxxxxxxxxxxxxxxxxxx",
        "username":"xxxxxxxx.xxxxx@shadkona.com"
    }
 

 #### Response 
 200 OK
 
#### Response Header
 
 **authorization** : Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIj
                     oic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV
                     4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.KEL-   
                     ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ
 

### 2.Api Call for getting the panchyat data(getContext())
**URL Structure**  : https://{hostname}/api/{apiVer}/CtxDto  

**URL:** https://ts.gramsevak.net/api/1/CtxDto

**Method :** GET
#### Headers  
> **Accept:** application/json  
 **Content-Type:** application/json  
 **Authorization:** Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXB
                pIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.  
                KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ 

### Request body : 
**Response Status :** 200 OK
#### Response : 

    {
        "stateId":"3f06af63-a93c-0001-9797-005056907001",
        "distId":null,
        "divId":null,
        "mandalId":null,
        "panchayatId":null,
        "stateName":null,
        "distName":null,
        "divName":null,
        "mandalName":null,
        "panchayatName":null,
        "docUrl":"https://www.shadkona.com",
        "videoUrl":"https://www.youtube.com/channel/UCQqCWfCwR-zo21w6N0Mb_sQ",
        "faqUrl":"https://www.shadkona.com/?page_id=458",
        "troubleshootingUrl":"https://www.shadkona.com/?page_id=500",
        "supportLine01":"+918019016669",
        "supportLine02":"+918019016668",
        "supportLine03":"+914042203915",
        "supportLine04":"+918096326342",
        "supportLine05":"+918019016668"
    }
    
     


### 3.API call for getting userSession

**URL Structure**  : https://{hostname}/api/{apiVer}/user/{userId}  

**URL**: https://ts.gramsevak.net/api/1/UserSessionDto 

**Method** : GET
#### Headers  : 
>**Accept:** application/json  
**Content-Type:** application/json  
**Authorization:** Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZW
 N1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2  
 FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJS
 T0xFX1NDT1BFX1NUQVRFIl19.KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-  
 EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ 

#### Request body : 
**Response Status** : 200 OK
#### Response : 

    {
        "sessionTimeout":900000,
        "offlineTimeout":604800000,
        "userId":"928ff18f-da12-49c6-af54-be5c3571a5ad",
        "userName":"Lanka Naga Sai Reddy",
        "designation":"Developer",
        "flushData":false,
        "profilePicUuid":null,
        "base64EncodedJpegImage":null
    }


### Flow of Login API Calls
{{<mermaid align="center">}}
graph TD 
	start((Start))
	loginApiCall{API Call : login}
	getContextApiCall{API Call : getContext}
	getUserSessionApiCall{API Call : getUserSession}
	mainActivity{mainActivity}
	error1>error]
	error2>error]
	error3>error]
	end1((end))
	start-->loginApiCall
	loginApiCall--Response!=200-->error1
	loginApiCall--Response==200-->getContextApiCall
	getContextApiCall--Response!=200-->error2
    getContextApiCall--Response==200-->getUserSessionApiCall
	getUserSessionApiCall--Response!=200-->error3
    getUserSessionApiCall--Response==200-->mainActivity
    mainActivity-->end1

	
{{< /mermaid >}}

### Login Module & GS-Cloud Operations :
#### [Routing API](http://localhost:1313/productspecification/features/mobileapplication/api/routing-api/)

{{<mermaid align="center">}}
sequenceDiagram
	participant Dashboard as Dashboard
	participant SQLite as SQLite Database
    participant Login as Login Module
    participant Net as Network Utils
    participant Route as GS-Route
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
        Login->>+Net: Check Internet , POST "https://{hostname}/api/login" InvokeAuthApi
        Net--x-Login: F : Connection Error
        Login->>+cloud: S : POST "https://{hostname}/api/login" InvokeAuthApi
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





