---
title: Panchayat Selection Api
tags : ["Composing"]
---

## API Call - URL Description
|API Call|Method|URL Endpoint|Description|
|-----------|--------|-------|-------------|
|getDistrictResult|GET|/api/{apiVer}/District/list|To get the district names of the state|
|getDivisionResult|GET|/api/{apiVer}/Division/list|To get the division names of the district|
|getMandalResult|GET|/api/{apiVer}/Mandal/list|To get the mandal names of the division|
|getPanchayatResult|GET|/api/{apiVer}/Panchayat/list|To get the panchayat names of the mandal|
|panchayatSurveyStart|GET|/api/{apiVer}/PanchayatSurveyStart|To get the PanchayatSurveyStart data ex:totalAssetCount,currentPanchyatAssetCount,totalPanchayatCount..e.t.c|                                                                                                        
|login|PUT|/api/login|To authenticate the user|
|getContext|GET|/api/1/CtxDto|To get the panchayat data ex: State, District, Division, Mandal, Panchayat etc..|

### Description :

1. On Creation of the Panchyat Selection Page we have to Load the User from the local Data Base.

2. After loading the user from the Data Base,Then invoke the **getDistrictResult(https://{hostname}/api/{apiVer}/District/list/{StateId})** API call.
    - 2.1 If the response is 200 - Then store all the district names from the API Response into districtNames arrayList,and go to step 3.
    - 2.2 If the response is 401 - Then check  failedToken value and, if it is equal to unsuccessful then navigate the user to the login page for re-login. After successful login repeat step 1.
    - 2.3 If response is 401 & failedToken value is null then get the user object from database and invoke login API( invokeAuthApi(DISTRICT)) calls steps 1 & 2 in login API - reference for Login API step 1,2 [Login API](http://localhost:1313/productspecification/features/mobileapplication/api/login-api/)
          After login api success repeat step 1.
    - 2.4 If response is 400 or any other code - show error message

3. After succession of getDistrictResults API Call,User selects the one district from the district spinner.  
   Based on district id,Invoke the **getDivisionResult(https://{hostname}/api/{apiVer}/Division/list/{DistrictId})** API Call.
    - 3.1 If the response is 200 - Then store all the division names from the API Response into divisionNames arrayList,and go to step 4.
    - 3.2 If the response is 401 - Then check  failedToken value and, if it is equal to unsuccessful then navigate the user to the login page for re-login. After successful login repeat step 1.
    - 3.3 If response is 401 & failedToken value is null then get the user object from database and invoke login API( invokeAuthApi(DIVISION)) calls steps 1 & 2 in login API - reference for Login API step 1,2 [Login API](http://localhost:1313/productspecification/features/mobileapplication/api/login-api/)
      After login api success repeat step 1.
    - 3.4 If response is 400 or any other code - show error message

4. After succession of getDivisionResult API Call,User selects the one division from the division spinner.  
   Based on division id, Invoke the **getMandalResult(https://{hostname}/api/{apiVer}/Mandal/list/{DivisionId})** API Call.
    - 4.1 If the response is 200 - Then store all the mandal names from the API Response into mandalNames arrayList,and go to step 5.
    - 4.2 If the response is 401 - Then check  failedToken value and, if it is equal to unsuccessful then navigate the user to the login page for re-login. After successful login repeat step 1.
    - 4.3 If response is 401 & failedToken value is null then get the user object from database and invoke login API( invokeAuthApi(MANDAL)) calls steps 1 & 2 in login API - reference for Login API step 1,2 [Login API](http://localhost:1313/productspecification/features/mobileapplication/api/login-api/)
      After login api success repeat step 1.
    - 4.4 If response is 400 or any other code - show error message

5. After succession of getMandalResult API Call,User selects the one mandal from the mandal spinner.  
   Based on mandal id, Invoke the **getPanchayatResult( https://{hostname}/api/{apiVer}/Panchayat/list/{MandalId})** API Call.
    - 5.1 If the response is 200 - Then store all the mandal names from the API Response into mandalNames arrayList,and go to step 6.
    - 5.2 If the response is 401 - Then check  failedToken value and, if it is equal to unsuccessful then navigate the user to the login page for re-login. After successful login repeat step 1.
    - 5.3 If response is 401 & failedToken value is null then get the user object from database and invoke login API( invokeAuthApi(PANCHAYAT)) calls steps 1 & 2 in login API - reference for Login API step 1,2 [Login API](http://localhost:1313/productspecification/features/mobileapplication/api/login-api/)
      After login api success repeat step 1.
    - 5.4 If response is 400 or any other code - show error message

6. After succession of getPanchayatResult API Call,User selects the one panchayat from the panchayat spinner.  
   Based on panchayat id, Invoke the **panchayatSurveyStart(https://{hostname}/api/{apiVer}/PanchayatSurveyStart/{PanchyatId})** API Call.
    - 6.1 If the response is 200 - Then store all the data from the API Response into DashboardPreference.
    - 6.2 If the response is 401 - Then check  failedToken value and, if it is equal to unsuccessful then navigate the user to the login page for re-login. After successful login repeat step 1.
    - 6.3 If response is 401 & failedToken value is null then get the user object from database and invoke login API(invokeAuthApi(START_PANCHAYAT_SURVEY)) calls steps 1 & 2 in login API - reference for Login API step 1,2 [Login API](http://localhost:1313/productspecification/features/mobileapplication/api/login-api/)
      After login api success repeat step 1.
    - 6.4 If response is 400 or any other code - show error message


### 1.API call for loading  all districts based on state id.
**URL Structure:**  https://{hostname}/api/{apiVer}/District/list/{StateId}
 
**URL:** https://ts.gramsevak.net/api/1/District/list?id=3f06af63-a93c-11e4-9797-005056907001
 
**Method** : GET

#### Headers : 
 
 >**Accept:** application/json  
 **Content-type:** application/json  
 **s-jwt-token:** HZFE5EE0CE27304187B618B92A38AEC771

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
           "data":
           [
              {
                "id":"b5218ae8-89bd-4ccf-9f9f-bb94ab019902",
                "value":"Bangalore"
              }
           ]

   }
        
        
        
        
### 2.API call for loading  all divisions based on district id.

**URL Structure:**  https://{hostname}/api/{apiVer}/Division/list/{DistrictId}

**URL:** https://ts.gramsevak.net/api/1/Division/list?id=3f06af63-a93c-11e4-9797-005056907102
 
**Method** : GET

#### Headers : 
 
 >**Accept:** application/json  
 **Content-type:** application/json  
 **s-jwt-token:** HZFE5EE0CE27304187B618B92A38AEC771

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
            "data":
            [
                {
                    "id":"12b2d041-006f-40a0-8c59-71e77330fb2a",
                    "value":"Bangalore Urban"
                }
            ]

     }




### 3.API call for loading  all mandals based on division id.

**URL Structure:**  https://{hostname}/api/{apiVer}/Mandal/list/{DivisionId}

**URL:** https://ts.gramsevak.net/api/1/Mandal/list?id=3f06af63-a93c-11e4-9797-005056907103
 
**Method** : GET

#### Headers : 
 
 >**Accept:** application/json  
 **Content-type:** application/json  
 **s-jwt-token:** HZFE5EE0CE27304187B618B92A38AEC771

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
        "data":
            [
                {
                    "id":"d7e347d0-2573-49da-a5ad-db6a5e0b5a83",
                    "value":"Anekal"
                }
            ]
      }
 
 
 ### 4.API call for loading  all panchyats based on mandal id.
 
 **URL Structure:**  https://{hostname}/api/{apiVer}/Panchayat/list/{MandalId}
 
 **URL:** https://ts.gramsevak.net/api/1/Panchayat/list?id=3f06af63-a93c-11e4-9797-005056907103
  
 **Method** : GET
 
 #### Headers : 
  
  >**Accept:** application/json  
  **Content-type:** application/json  
  **s-jwt-token:** HZB040F723510E49768A6F1FB60572CDB5
 
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
            "data":
            [
                {
                    "id":"9af13692-af5c-41e2-88e4-ed91a7e5c9c5",
                    "value":"chandapura"
                },
                {
                    "id":"b1b0af00-f15f-400e-8d19-89ce6a761147",
                    "value":"ballur"
                }
            ]
       }
        
### 5.API call for Panchayat Survey Start details
 
 **URL Structure:** https://{hostname}/api/{apiVer}/PanchayatSurveyStart/{PanchyatId}
 
 **URL:** https://ts.gramsevak.net/api/1/PanchayatSurveyStart?id=3f06af63-a93c-11e4-9797-005056907006
  
 **Method** : GET
 
 #### Headers : 
  
  >**Accept:** application/json  
  **Content-type:** application/json  
  **s-jwt-token:**  HZB040F723510E49768A6F1FB60572CDB5
 
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
            "randomNumber":1631082566318,
            "todayAssetCount":0,
            "yesterdayAssetCount":1,
            "weekAssetCount":113,
            "monthAssetCount":120,
            "yearAssetCount":120,
            "totalAssetCount":120,
            "totalPanchayatCount":0,
            "avgAssetTimeMin":74555,
            "currentPanchyatAssetCount":null,
            "currentPanchayatHouseCount":1,
            "currentPanchayatKolagaramCount":1,
            "currentPanchayatAdvertisementCount":5,
            "currentPanchayatTradeLicenseCount":1,
            "currentPanchayatAuctionCount":0,
            "currentPanchayatVacantLandCount":117,
            "updatedTime":1631082566334,
            "errorMultipleOrg":false,
            "currentPanchayatId":"9af13692-af5c-41e2-88e4-ed91a7e5c9c5"
            ,"panchayatName":"chandapura",
            "mandalName":"Anekal",
            "divisionName":"Bangalore Urban",
            "districtName":"Bangalore",
            "stateName":"Telangana",
            "landSurveyNumber":"201,203,204,205,209"
        }

### Flow of Panchyat Selection API Calls
{{<mermaid align="center">}}
graph TD 
        start((Start))
        districtApiCall{API Call : getDistrictResult}
        divisionApiCall{API Call : getDivisionResult}
        mandalApiCall{API Call : getMandalResult}
        panchayatApiCall{API Call : getPanchayatResult}
        panchayatSurveyStart{API Call : PanchayatSurveyStart}
        getLoginApiCall{API Call : login}
        getContextApiCall{API Call : getContext}
        ResponseFailedToken{Response FailedToken}
        FailedTokenUnSuccessCheck{FailedToken == unsuccessful}
        ResponseFailedToken1{Response FailedToken}
        FailedTokenUnSuccessCheck1{FailedToken == unsuccessful}
        loadUserObjectFromDB[(Load User Object From DB)]
        storeResultsInDistrictArrayList[Store Results in District  Array List]
        storeResultsInDivisionArrayList[Store Results in Division  Array List]
        storeResultsInMandalArrayList[Store Results in Mandal  Array List]
        storeResultsInPanchyatArrayList[Store Results in Panchayat  Array List]
        LoginPage[LoginPage]
        StoreDataInKVDB[Store Panchyat data in KV Database]
        checkMethodLoader[checkMethodLoader]
        gotoDistrictApiCall[Go to district Api Call]
        gotoDivisionApiCall[Go to division Api Call]
        gotoMandalApiCall[Go to mandal Api Call]
        gotoPanchyatApiCall[Go to panchayat Api Call]
        gotoPanchayatSurveyStartApiCall[Go to panchayat Survey Start Api Call]
    	error1>error]
    	error2>error]
    	error3>error]
    	error4>error]
    	error5>error]
    	error6>error]
    	end1((End))
    	end2((End))
    	    
    	    start-->loadUserObjectFromDB
    	    
            loadUserObjectFromDB-->districtApiCall
            districtApiCall--Response==200-->storeResultsInDistrictArrayList
            districtApiCall--Response==401-->ResponseFailedToken
            districtApiCall--Response=!200 and Response!=401-->error1
            	
            storeResultsInDistrictArrayList--clickOnDistrictSpinner-->divisionApiCall
            divisionApiCall--Response==200-->storeResultsInDivisionArrayList
            divisionApiCall--Response==401-->ResponseFailedToken
            divisionApiCall--Response=!200 and Response!=401-->error2
            
            storeResultsInDivisionArrayList--clickOnDivisionSpinner-->mandalApiCall
            mandalApiCall--Response==200-->storeResultsInMandalArrayList
            mandalApiCall--Response==401-->ResponseFailedToken
            mandalApiCall--Response=!200 and Response!=401-->error3
            
            storeResultsInMandalArrayList--clickOnMandalSpinner-->panchayatApiCall
            panchayatApiCall--Response==200-->storeResultsInPanchyatArrayList
            panchayatApiCall--Response==401-->ResponseFailedToken
            panchayatApiCall--Response=!200 and Response!=401-->error4
            
            storeResultsInPanchyatArrayList--clickOnContinueSurveyBtn-->panchayatSurveyStart
            panchayatSurveyStart--Response==200-->storeResultsInDashboardPreference
            panchayatSurveyStart--Response==401-->ResponseFailedToken
            panchayatSurveyStart--Response=!200 and Response!=401-->error5     
               
            subgraph 401 Page
                ResponseFailedToken--NotNULL-->FailedTokenUnSuccessCheck
                FailedTokenUnSuccessCheck--true-->LoginPage
                ResponseFailedToken--Null-->getLoginApiCall
                getLoginApiCall--Response==200-->getContextApiCall
                getLoginApiCall--Response==401-->ResponseFailedToken1
                ResponseFailedToken1--NotNULL-->FailedTokenUnSuccessCheck1
                FailedTokenUnSuccessCheck1--true-->LoginPage
                getContextApiCall--Response==200-->StoreDataInKVDB
                StoreDataInKVDB-->checkMethodLoader
                getContextApiCall--Response!=200-->error6
                checkMethodLoader--DISTRICT-->gotoDistrictApiCall
                checkMethodLoader--DIVISION-->gotoDivisionApiCall
                checkMethodLoader--MANDAL-->gotoMandalApiCall
                checkMethodLoader--PANCHAYAT-->gotoPanchyatApiCall
                checkMethodLoader--STARTPANCHAYATSURVEY-->gotoPanchayatSurveyStartApiCall       
            end
            storeResultsInDashboardPreference-->end1
            LoginPage-->end2
   
       
        
    	
	
{{< /mermaid >}}



### Sequence Diagram :
{{<mermaid align="center">}}
sequenceDiagram
	participant LoginPage as LoginPage
	participant KVDB as KV Database
	participant SQLite as SQLite Database
    participant PanchayatSelection as PanchayatSelection Module
    participant Net as Network Utils
    participant cloud as GS-Cloud
    autonumber
    
    rect rgb(244,244,244)
        PanchayatSelection->>SQLite: loadUserObjectFromDB
        SQLite-->>PanchayatSelection:Getting the User Object
        PanchayatSelection->>+Net:Check Internet , GET/api/{apiVer}/District/list/{StateId} getDistrictResult
        Net--X-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : GET/api/{apiVer}/District/list/{StateId} getDistrictResult
        cloud-->>-PanchayatSelection: RES 200 {store results in array list}
        Note right of PanchayatSelection:go to step 8 while selection of district from spinner.
        cloud-->>PanchayatSelection: RES 401{go to Step 29 Note }
       
    end   
    rect rgb(244,244,244)
        PanchayatSelection->>+Net:Check Internet , GET/api/{apiVer}/Division/list/{DistictId} getDivisionResult
        Net--X-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : GET/api/{apiVer}/Division/list/{DistictId} getDivisionResult
        cloud-->>-PanchayatSelection: RES 200 {store results in array list}
        Note right of PanchayatSelection:go to step 13 while selection of division from spinner.
        cloud-->>PanchayatSelection: RES 401{go to Step 29 Note }
           
    end   
    
    rect rgb(244,244,244)
        PanchayatSelection->>+Net:Check Internet , GET/api/{apiVer}/Mandal/list/{DivisionId} getMandalResult
        Net--X-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : GET/api/{apiVer}/Mandal/list/{DivisionId} getMandalResult
        cloud-->>-PanchayatSelection: RES 200 {store results in array list} 
        Note right of PanchayatSelection:go to step 18 while selection of mandal from spinner.  
        cloud-->>PanchayatSelection: RES 401{go to Step 29 Note }
    end   
    rect rgb(244,244,244)
        PanchayatSelection->>+Net:Check Internet , GET/api/{apiVer}/Panchayat/list/{MandalId} getPanchayatResult
        Net--X-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : GET/api/{apiVer}/Panchayat/list/{MandalId} getPanchayatResult
        cloud-->>-PanchayatSelection: RES 200  {store results in array list}    
        Note right of PanchayatSelection:go to step 23 while selection of panchyat from spinner and click on continueSurvey Button.
        cloud-->>PanchayatSelection: RES 401{go to Step 29 Note }
    end   
    
    rect rgb(244,244,244)
        PanchayatSelection->>+Net:Check Internet , GET/api/{apiVer}/PanchayatSurveyStart/{PanchayatId} panchayatSurveyStart
        Net--X-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : GET/api/{apiVer}/PanchayatSurveyStart/{PanchayatId} panchayatSurveyStart
        cloud-->>-PanchayatSelection: RES 200  
        PanchayatSelection-->>KVDB: Store PanchayatSurveyStart details in KVDB.
        cloud-->>PanchayatSelection: RES 401{go to step 29 Note}
    end 
    
    rect rgb(244,244,244)
        Note right of PanchayatSelection: from step 7/12/17/22/28 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
        Note right of PanchayatSelection: if (failedToken != null) { if(failedToken.equals("unsuccessful"){go to step 29 }}else { go to 30 }
        PanchayatSelection->>LoginPage: navigate to Login Page   
    end  
    
    rect rgb(244,244,244)
        PanchayatSelection->>+Net: Check Internet , POST api/login InvokeAuthApi
        Net--x-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : POST /api/login InvokeAuthApi
        cloud-->>-PanchayatSelection: RES 200 {go to step 36 }
        cloud-->>PanchayatSelection: RES 401 
    end 
    
    rect rgb(244,244,244)
        Note right of PanchayatSelection: from step 34 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
        Note right of PanchayatSelection: if (failedToken != null) { if(failedToken.equals("unsuccessful"){go to step 35 }} 
        PanchayatSelection->>LoginPage: navigate to Login Page
    end   
    
    rect rgb(244,244,244)
        PanchayatSelection->>+Net: Check Internet , api/{apiVer}/CtxDto GetContext
        Net--x-PanchayatSelection: F : Connection Error
        PanchayatSelection->>+cloud: S : GET api/{apiVer}/CtxDto GetContext
        cloud-->>-PanchayatSelection: RES 200
        PanchayatSelection-->>KVDB: Store Panchyat Data on KV Database.
        Note right of PanchayatSelection:if (checkMethodLoader==DISTRICT) { go to step 3 }
        Note right of PanchayatSelection: else if(checkMethodLoader==DIVISION) { go to step 8}
        Note right of PanchayatSelection: else if(checkMethodLoader==MANDAL) { go to step   13 }
        Note right of PanchayatSelection: else if(checkMethodLoader==PANCHAYAT) { go to step  18  }
        Note right of PanchayatSelection: else if(checkMethodLoader==START_PANCHAYAT_SURVEY) {go to step 23 }      
    end 

    
   
          
{{< /mermaid >}}



