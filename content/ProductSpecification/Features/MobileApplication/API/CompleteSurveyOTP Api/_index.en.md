---
title: CompleteSurveyOTP Api
tags : ["Composing"]
---


### 1.Api call surveyStopOtpReq
**URL Structure**  : https://{hostname}/api/1/PanchayatSurveyEndReq  

**URL:** https://ts.gramsevak.net/api/1/PanchayatSurveyEndReq

**Method :** GET
#### Headers  
> **Accept:** application/json  
 **Content-Type:** application/json  
 **Authorization:** Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXB
                pIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.  
                KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ  
 **s-jwt-token** : ST4FE03FB3FD58E90E30904BB6DC9A995B  

### Request body : No Request Body
### Response Header
set-cookie: JSESSIONID=4233552073012F9D62CBE4C3A6792A5E; Path=/; Secure; HttpOnly
set-cookie: hazelcast.sessionId=HZ4FE0390E30904FBBB3FD58E6DC9A995F; Path=/
**Response Status :** 200 OK
#### Response : 

    {
        "otpUuid":"674f7fc5-25de-43cd-b1fa-9f99742be2de",
        "otpTxId" : "NGHQ",
        "smsCode" : "587019",
        "emailCode" : "587019",
        "resend" : false
    }
    

### 2.Api Call login
 **URL Structure:**  https://{hostname}/api/login
 
 **URL:**  https://ts.gramsevak.net/api/login
 
 **Method** : POST
 
 #### Headers : 
 
 >**Accept:** application/json  
 **Content-type:** application/json
 
 #### Request body  :
 
    {
        "password":"xxxxxxxxxxxxxxxxxxxxxxxxxxx",  
        "username":"xxxxxxxxxxx.xxxxx@shadkona.com"  
    }
 

 #### Response 
 200 OK
 
#### Response Header
 
 **authorization** : Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6Im9wZW5hcGlAbG9jYWwuY29tIiwiZXhwIjoxNTkwMDM3MjUxLCJyb2wiOlsiUk9MRV9TVVJWRVlfVVNFUl9DUkVBVEUiLCJST0xFX1NVUlZFWV9VU0VSX1ZJRVciXX0.zbhkNRbkvfcpWYU5Nwx8ZOjw9yYyubBYiEsdyrPdGEQpCkJu_BvfT1Jw1jaYbKE2OUGOx1LBhnRVZ_zoQDEzFA  
 **s-jwt-token** : ST4FE03FB3FD58E90E30904BB6DC9A995B
 

### 3.Api call getContext
**URL Structure**  : https://{hostname}/api/{apiVer}/CtxDto  

**URL:** https://ts.gramsevak.net/api/1/CtxDto

**Method :** GET
#### Headers  
> **Accept:** application/json  
 **Content-Type:** application/json  
 **Authorization:** Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXB
                pIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.  
                KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ  
 **s-jwt-token** : ST4FE03FB3FD58E90E30904BB6DC9A995B  

### Request body : No Request Body
### Response Header
set-cookie: JSESSIONID=4233552073012F9D62CBE4C3A6792A5E; Path=/; Secure; HttpOnly
set-cookie: hazelcast.sessionId=HZ4FE0390E30904FBBB3FD58E6DC9A995F; Path=/
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
    
     


### 4.Api Call panchayatSurveyEnd
 **URL Structure:**  https://{hostname}/{apiVersion}//PanchayatSurveyEnd
 
 **URL:**  https://ts.gramsevak.net/1/PanchayatSurveyEnd
 
 **Method :** GET
 #### Headers  
 > **Accept:** application/json  
  **Content-Type:** application/json  
  **Authorization:** Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXB
                 pIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6ImFkbWluQGxvY2FsLmNvbSIsImV4cCI6MTU4NDExODMzNSwicm9sIjpbIlJPTEVfQWRtaW4iLCJST0xFX1NDT1BFX1NUQVRFIl19.  
                 KEL-ugUdRkLcPhYod1BvpM3nbtru31r31wGjJA5iSqYaieK7e-EWNNOWg4OwVm_76JEogjNET7g8psGPTAaayQ  
  **s-jwt-token** : ST4FE03FB3FD58E90E30904BB6DC9A995B  
 
 ### Request body : No Request Body
 ### Response Header
 set-cookie: JSESSIONID=4233552073012F9D62CBE4C3A6792A5E; Path=/; Secure; HttpOnly
 set-cookie: hazelcast.sessionId=HZ4FE0390E30904FBBB3FD58E6DC9A995F; Path=/
 
 **Response Status :** 200 OK
 
 #### Response : 
 
     {
         
     }
 
 

  


### Flow of SignUp API Calls
#### [Routing API](http://localhost:1313/productspecification/features/mobileapplication/api/routing-api/)  
{{<mermaid align="center">}}
graph TD 
	start((Start))
	ApiCallSurveyStopOtpReq{API Call: SurveyStopOtpReq}
	PerformOperation[PreferenceHelper.IS_STOP_SURVEY_ACTION = true]
	FailedTokenNullCheck1{FailedToken}
	FailedTokenEqualCheck1{FailedToken == UNSUCCESS_TOKEN}
	error1>error]
	LoginPage1[Login Page]
	DBCallLoadUserById[Database Call: loadUserById]
	ApiCallInvokeAuthApi{API Call: InvokeAuthApi}
    FailedTokenNullCheck2{FailedToken}
	FailedTokenEqualCheck2{FailedToken == UNSUCCESS_TOKEN}
	error2>error]
	LoginPage2[Login Page]
	ApiCallGetContext{API Call: GetContext}
	SurveyCompleteEqualCheck{serviceCallDecide == SURVEY_COMPLETE}
	ValidateOtpEqualCheck{serviceCallDecide == VALIDATE_OTP}
	GotoApiCallSurveyStopOtpReq[go to API Call: SurveyStopOtpReq]
	ApiCallPanchayatSurveyEnd{API Call: panchayatSurveyEnd}
	NavigateToSurveyCompletedPage[SurveyCompleted Page]
	DisplayApiErrorMessages>Display Respective Api ErrorMessages]
    FailedTokenNullCheck3{FailedToken}
	FailedTokenEqualCheck3{FailedToken == UNSUCCESS_TOKEN}	
	LoginPage3[Login Page]
	end1((end))
	
	start-->ApiCallSurveyStopOtpReq
	ApiCallSurveyStopOtpReq--Response==200-->PerformOperation
	ApiCallSurveyStopOtpReq--Response==401-->FailedTokenNullCheck1
    ApiCallSurveyStopOtpReq--Response!=Other-->error1
    
    FailedTokenNullCheck1--NULL-->FailedTokenEqualCheck1
    FailedTokenNullCheck1--NOT NULL-->DBCallLoadUserById

	FailedTokenEqualCheck1-->LoginPage1
	
	DBCallLoadUserById-->ApiCallInvokeAuthApi
    
    ApiCallInvokeAuthApi--Response==200-->ApiCallGetContext
    ApiCallInvokeAuthApi--Response==401-->FailedTokenNullCheck2
    ApiCallInvokeAuthApi--Response!=Other-->error2
    
    FailedTokenNullCheck2--NULL-->FailedTokenEqualCheck2
    
    FailedTokenEqualCheck2-->LoginPage2
    
    ApiCallGetContext--Response==200-->SurveyCompleteEqualCheck
    SurveyCompleteEqualCheck--YES-->GotoApiCallSurveyStopOtpReq
    SurveyCompleteEqualCheck--NO-->ValidateOtpEqualCheck
    ValidateOtpEqualCheck-->ApiCallPanchayatSurveyEnd
    
    ApiCallPanchayatSurveyEnd--Response==200-->NavigateToSurveyCompletedPage
    NavigateToSurveyCompletedPage-->end1
    ApiCallPanchayatSurveyEnd--Response==400-->DisplayApiErrorMessages
    
    ApiCallPanchayatSurveyEnd--Response==401-->FailedTokenNullCheck3
    
    FailedTokenNullCheck3--NULL-->FailedTokenEqualCheck3
    FailedTokenNullCheck3--NOT NULL-->DBCallLoadUserById
    
    FailedTokenEqualCheck3-->LoginPage3
	
{{< /mermaid >}}


### Sequence Diagram :

{{<mermaid align="center">}}
sequenceDiagram
    participant SurveySuccess as SurveySuccessPage
    participant Login as Login
	participant SQLite as SQLite Database
	participant CompleteSurvey as CompleteSurvey OTP
    participant Net as Network Utils
    participant Cloud as GS-Cloud
    autonumber
    
    rect rgb(244,244,244)
        CompleteSurvey->>+Net: Check Internet , GET api/1/PanchayatSurveyEndReq surveyStopOtpReq
        Net--x-CompleteSurvey: F : Connection Error
        CompleteSurvey->>+Cloud: S : GET api/1/PanchayatSurveyEndReq surveyStopOtpReq
        Cloud-->>-CompleteSurvey: RES 200 {perform below operation }
        Note right of CompleteSurvey: PreferenceHelper.IS_STOP_SURVEY_ACTION = true
        CompleteSurvey->>+Cloud: S : GET api/1/PanchayatSurveyEndReq surveyStopOtpReq
        Cloud-->>-CompleteSurvey: RES 401 
    end  
    
    rect rgb(244,244,244)
        Note right of CompleteSurvey: from step 6 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
        Note right of CompleteSurvey: if (failedToken != null) { if(failedToken.equals("unsuccessful"){go to step 7 }} else { go to step 8 }
        CompleteSurvey->>Login: navigate to Login Page
    end
    
    rect rgb(244,244,244)
        CompleteSurvey->>+SQLite: loadUserById
        SQLite-->>-CompleteSurvey: User Object   
    end
    
    rect rgb(244,244,244)
        CompleteSurvey->>+Net: Check Internet , POST api/login InvokeAuthApi
        Net--x-CompleteSurvey: F : Connection Error
        CompleteSurvey->>+Cloud: S : POST /api/login InvokeAuthApi
        Cloud-->>-CompleteSurvey: RES 200 {go to step 17}
        CompleteSurvey->>+Cloud: S : POST api/login InvokeAuthApi
        Cloud-->>-CompleteSurvey: RES 401
    end
    
    rect rgb(244,244,244)
        Note right of CompleteSurvey: from step 15 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
        Note right of CompleteSurvey: if (failedToken != null) { if(failedToken.equals("unsuccessful"){go to step 16 }}
        CompleteSurvey->>Login: navigate to Login Page
    end       
    
    rect rgb(244,244,244)
        CompleteSurvey->>+Net: Check Internet , api/{apiVer}/CtxDto GetContext
        Net--x-CompleteSurvey: F : Connection Error
        CompleteSurvey->>+Cloud: S : GET api/{apiVer}/CtxDto GetContext
        Cloud-->>-CompleteSurvey: RES 200
        Note right of CompleteSurvey: if ( serviceCallDecide.equals(SURVEY_COMPLETE) ) { go to step 1 }
        Note right of CompleteSurvey: else if(serviceCallDecide.equals(VALIDATE_OTP)){ go to step 21 }
    end  
    
    rect rgb(244,244,244)
        CompleteSurvey->>+Net: Check Internet , GET api/{apiVer}/PanchayatSurveyEnd panchayatSurveyEnd
        Net--x-CompleteSurvey: F : Connection Error
        CompleteSurvey->>+Cloud: S : GET api/{apiVer}/PanchayatSurveyEnd panchayatSurveyEnd
        Cloud-->>-CompleteSurvey: RES 200 {go to step 25 }
        CompleteSurvey->>SurveySuccess: navigate to Survey Completed Page
        CompleteSurvey->>+Cloud: S : GET api/{apiVer}/PanchayatSurveyEnd panchayatSurveyEnd
        Cloud-->>-CompleteSurvey: RES 401 {perform below checks }
        Note right of CompleteSurvey: from step 26 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
        Note right of CompleteSurvey: if (failedToken != null) { if(failedToken.equals("unsuccessful"){go to step 7 }} else { go to step 8 }
        CompleteSurvey->>+Cloud: S : GET api/{apiVer}/PanchayatSurveyEnd panchayatSurveyEnd
        Cloud-->>-CompleteSurvey: RES 400
        Note right of CompleteSurvey: Display respective api error message based on api error code
    end  
       
    
    
       
        
          
{{< /mermaid >}}

## API Call - URL Description
|API Call|Method|URL Endpoint|Description|
|-----------|--------|-------|-------------|
|surveyStopOtpReq|GET|api/1/PanchayatSurveyEndReq |To get the mobile and email OTP|
|login|POST|/api/login|To authenticate the user|
|getContext|GET|/api/1/CtxDto|To get the panchayat data ex: State, District, Division, Mandal, Panchayat etc..|
|surveyUser|GET|/{apiVersion}/PanchayatSurveyEnd |To Put the survey user in the server|

