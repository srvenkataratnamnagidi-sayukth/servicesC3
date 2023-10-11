---
title: Dashboard Api
tags : ["Composing"]
---

## API Call - URL Description
|API Call|Method|URL Endpoint|Description|
|-----------|--------|-------|-------------|
|getDashboard|GET|/api/${apiVer}/DashboardSummary|To get the survey summary details ex:Today Asset Count|
|login|PUT|/api/login|To authenticate the user|
|getContext|GET|/api/1/CtxDto|To get the panchayat data ex: State, District, Division, Mandal, Panchayat etc..|

### Description
1. In the Dashboard screen invoke the api call (1) dashboardSummary (https://{hostname}/api/${apiVer}/DashboardSummary) API
   - If the response is 200 - save the response data to dashboard preference and render the data in the dashboard screen
2. If the response is other than 200  
   - 2.1 If response is 401 - check failedToken value and it is equal to unsuccessful then navigate the user to the login page for re-login. After successful login repeat step 1  
   - 2.2 If response is 401 & failedToken value is null then get the user object from database and invoke login API calls steps 1 & 2 in login API - reference for Login API step 1,2 [Login API](http://localhost:1313/productspecification/features/mobileapplication/api/login-api/)
   After login api success repeat step 1  
   - 2.3 if response is 400 - show error message  
   

### 1.API call for getting  dashboard summary
**URL Structure:** https://{hostname}/api/${apiVer}/DashboardSummary
 
**URL:** https://ts.gramsevak.net/api/1/DashboardSummary
 
**Method** : GET

#### Headers : 
 
 >**Accept:** application/json  
 **Content-type:** application/json  

### Request body : 
>NA

#### Response Status 
 >200 OK
#### Response Header
>**Authorization:** Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXB
                pIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.  
                KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ 
#### Response : 
    {
       "captchaText":null,
       "randomNumber":1625664088577,
       "todayAssetCount":0,
       "weekAssetCount":0,
       "monthAssetCount":0,
       "yearAssetCount":0,
       "totalAssetCount":0,
       "totalPanchayatCount":0,
       "avgAssetTimeMin":10,
       "currentPanchyatAssetCount":null,
       "currentPanchayatHouseCount":0,
       "currentPanchayatKolagaramCount":0,
       "currentPanchayatAdvertisementCount":0,
       "currentPanchayatTradeLicenseCount":0,
       "currentPanchayatAuctionCount":0,
       "currentPanchayatVacantLandCount":0,
       "updatedTime":1594003811168,
       "errorMultipleOrg":true,
       "currentPanchayatId":"3f06af63-a93c-11e4-9797-005056907005",
       "panchayatName":"Bommaipalle",
       "mandalName":"Bangarupalem",
       "divisionName":"Chittor",
       "districtName":"Chittor",
       "stateName":"Telangana",
       "landSurveyNumber":null
    }
    
    


   

### Flow of Dashboard API Calls
{{<mermaid align="center">}}
graph TD 
	start((Start))
	dashboardApiCall{API Call : getDashboard}
	getContextApiCall{API Call : getContext}
	getLoginApiCall{API Call : login}
	ResponseFailedToken{Response FailedToken}
    FailedTokenUnSuccessCheck{FailedToken == unsuccessful}
    ResponseFailedToken1{Response FailedToken}
    FailedTokenUnSuccessCheck1{FailedToken == unsuccessful}
    gettingUserFromDB[(Get User From DB)]
    LoginPage[LoginPage]
    SetDataToDashBoarPage[Set data to dashboard page]
	error1>error]
	error2>error]
	error3>error]
	start-->dashboardApiCall
	dashboardApiCall--Response==200-->SetDataToDashBoarPage
	dashboardApiCall--Response==401-->ResponseFailedToken
	dashboardApiCall--Response=!200 and Response!=401-->error1
	ResponseFailedToken--NotNULL-->FailedTokenUnSuccessCheck
	FailedTokenUnSuccessCheck--true-->LoginPage
	ResponseFailedToken--Null-->gettingUserFromDB
	gettingUserFromDB-->getLoginApiCall
	getLoginApiCall--Response==200-->getContextApiCall
	getLoginApiCall--Response==401-->ResponseFailedToken1
	ResponseFailedToken1--NotNULL-->FailedTokenUnSuccessCheck1
    FailedTokenUnSuccessCheck1--true-->LoginPage
    getLoginApiCall--Response=!200 and Response!=401-->error2
    getContextApiCall--Response==200-->dashboardApiCall
    getContextApiCall--Response!=200-->error3
   
	
{{< /mermaid >}}



### Sequence Diagram :
{{<mermaid align="center">}}
sequenceDiagram
	participant LoginPage as LoginPage
	participant KVDB as KV Database
	participant SQLite as SQLite Database
    participant DashBoard as DashBoard Module
    participant Net as Network Utils
    participant cloud as GS-Cloud
    autonumber
    
    rect rgb(244,244,244)
        DashBoard->>+Net:  Check Internet,On Starting of the Dashboard page
        Net--x-DashBoard: F : Go to step 3
        DashBoard-->>SQLite:getCurrentSurveySummary
        SQLite-->>DashBoard: Display current summary details in DashBoard page.
        DashBoard-->>KVDB: get UI details from the KV DataBase(Update UI).
        KVDB-->>DashBoard: Display UI details in DashBoard page.
        DashBoard-->cloud: S : Go to step 8
         
    end   
    rect rgb(244,244,244)
         DashBoard->>+Net: Check Internet, GET /api/${apiVer}/DashboardSummary  getDashboard
         Net--x-DashBoard: F :Connection Error
         DashBoard->>+cloud: S :GET /api/${apiVer}/DashboardSummary  getDashboard
         cloud-->>-DashBoard: if(RES 200){go to step  12} else if(RES 401){go to step 16)
         
    end
    rect rgb(244,244,244)
        DashBoard-->>KVDB: Put all the data into KV DataBase which is get from GS-cloud.
        KVDB-->>DashBoard: Display UI Data in Dashboard Page
        DashBoard-->>SQLite:getCurrentSummaryData
        SQLite-->>DashBoard: Display current summary details in DashBoard page.
        
    end
        
    rect rgb(244,244,244)
        Note right of DashBoard: from step 11/22 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
        Note right of DashBoard: if (failedToken != null) { if(unsuccessful.equals("unsuccessful"){go to step 16 }} else { go to step 17 }
        DashBoard->>LoginPage: navigate to Login Page
    end
    
    rect rgb(244,244,244)
        DashBoard-->>SQLite: loadUserObjectFromDB
        SQLite-->>DashBoard: getting the User Object
        DashBoard->>+Net:  Check Internet , POST /api/login  login
        Net--x-DashBoard: F : Connection Error
        DashBoard->>+cloud: S :POST /api/login  login
        cloud-->>-DashBoard: if(RES 200) {go to step 14} else if(RES 401){go to step 16)
    
    end 
    rect rgb(244,244,244)
        DashBoard->>+Net:  Check Internet ,GET /api/1/CtxDto GetContext
        Net--x-DashBoard: F : Connection Error
        DashBoard->>+cloud: S : GET /api/1/CtxDto GetContext
        cloud-->>-DashBoard: RES 200 {go to step 27 }
        DashBoard-->>KVDB:Store panchyat(getContex) data in KV DataBase.
        KVDB-->>DashBoard:Go to Step 8.
        
    end   
   
          
{{< /mermaid >}}



