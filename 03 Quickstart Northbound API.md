# Quickstart ALLIoT Northbound API

You can use Postman for testing the API
https://www.getpostman.com/

API Url: https://160.44.201.125:8743

## Setup Postman  
Open Settings  
1. General  
* SSL Verification off  
2. Certificates --->   Add Certificate  
* Host: 160.44.201.125:8743
* CRT File --> choose "plt-app-gw.crt" from Northbound API Folder
* Key File --> choose "plt-app-key.crt" from Northbound API Folder
* Password: IoT2018@HW

No you need the APP_ID and Password from (01 Quickstart ALLIoT)

## Login

2.1 Secure Access of Applications (Northbound API.pdf / Page 6)  
### Request
POST `https://160.44.201.125:8743/iocm/app/sec/v1.1.0/login`  
`Content-Type:application/x-www-form-urlencoded   `
```
Body: 
{ 
    appId=******&secret=****** 
}
```
### Response
```
Status Code: 200 OK   
Content-Type: application/json  
Body: 
{ 
    "scope": "default", 
    "tokenType": "bearer", 
    "expiresIn": "*******", 
    "accessToken": "*******",
    "refreshToken": "*******"
}
```

In all other request you need the **accessToken**, **deviceId** and the **appId** 

## Get Device Info
2.9.2 Query Information About a Device (Northbound API.pdf / Page  194)
### Request
GET `https://160.44.201.125:8743/iocm/app/dm/v1.3.0/devices/{deviceId}?appId={appId}`
```
Header:   
"app_key: <<appId>
"Authorization:Bearer <<accessToken>> 
Content-Type:application/json;
```

## Get Device Data
2.9.8 Query Historical Device Data (Northbound API.pdf / Page 207)


## Send Device Commands
2.11.12 Create a Device Command (V4) (Northbound API.pdf / Page  320)

### Request
POST `https://160.44.201.125:8743/iocm/app/cmd/v1.4.0/deviceCommands`
```
Header:   
"app_key: <<appId>
"Authorization:Bearer <<accessToken>> 
Content-Type:application/json;
```
Body for StringCommand:    
```
{    
  "deviceId": <<deviceID>>,
  "command": {
    "serviceId": "StringData",
    "method": "StringCmd",
    "paras": {
      "StringParamKey": "<<Key>>"
      "StringParamValue": "<<Value>>"
      
    }
  }
}
```

Body for IntCommand:  
```
{    
  "deviceId": <<deviceID>>,
  "command": {
    "serviceId": "IntData",
    "method": "IntCmd",
    "paras": {
      "IntParamKey": "<<Key>>"
      "IntParamValue": <<Value>>
      
    }
  }
}
```

### Response

```
{
    "commandId": "xxx",
    "appId": "<<appId>>",
    "deviceId": "<<deviceId>>",
    "command": {
        "serviceId": "xxx",
        "method": "xx",
        "paras": {
            "xx": yyy
        }
    },
    "expireTime": 172800,
    "status": "PENDING",
    "creationTime": "xxx",
    "issuedTimes": 0
}
```



## Query Device Commands
2.11.13 Query Device Commands (V4)  (Northbound API.pdf / Page  326)

### Request

GET `https://160.44.201.125:8743/iocm/app/cmd/v1.4.0/deviceCommands?pageNo=0&pageSize=10&deviceId=<<deviceId>&startTime=YYYYMMDDTHHmmssZ&endTime=YYYYMMDDTHHmmssZ`

### Response
Example on Northbound API.pdf / Page  329
