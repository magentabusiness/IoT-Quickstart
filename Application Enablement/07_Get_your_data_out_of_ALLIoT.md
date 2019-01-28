# How to get your data out of ALLIoT

Be sure that you have a valid accessToken, otherwise Login again.  
[Connect to the Rest API](06_Connect_to_REST_API.md)

## Get all devices of your application

1. Select `02 Get Devices`from the ALLIoT Demo Connection
2. Press "Send"

Detail: 
GET Request to URL with access Token  
`https://{{server}}/iocm/app/dm/v1.3.0/devices?appId={{appId}}&pageNo=0&pageSize=10  `  

{{server}} and {{appId}} are Variables from your Environment.

Header:   
```
"app_key: <<appId>
"Authorization:Bearer <<accessToken>> 
Content-Type:application/json;
```

In the Response you should see a JSON Object with all your Devices.

Example Response:
```json
{
    "totalCount": 9,
    "pageNo": 0,
    "pageSize": 10,
    "devices": [
        {
            "deviceId": "3c9b523d-b17c-XXXX-97e0-64e1d05d1267",
            "gatewayId": "3c9b523d-b17c-XXX-97e0-64e1d05d1267",
            "nodeType": "GATEWAY",
            "createTime": "20190114T142233Z",
            "lastModifiedTime": "20190123T151214Z",
            "deviceInfo": {
                "nodeId": "357518080213275",
                
                ...
                ...
                ...
            }
        }
    ]
}
```




## Get historical Data of your device

NOTE: ALLIoT will only save your data up to 30 Days.  
In the last command you see this Line:  
`"deviceId": "3c9b523d-b17c-XXXX-97e0-64e1d05d1267"`  
**This is the unique DeviceID - for the next Request you have add this ID to your Environment to deviceId.**

1. Select `04 Get Historical Data from Device`from the ALLIoT Demo Connection
2. Press "Send"

Detail:
GET Request to URL:
https://{{server}}/iocm/app/data/v1.1.0/deviceDataHistory?deviceId={{deviceId}}&gatewayId={{deviceId}}&startTime=20181015T000000Z&endTime=20291015T000000Z&appId={{appId}}

{{server}}, {{appId}} and {{deviceId}} are Variables from your Environment.
The time period can be set via the parameters startTime and endTime.

Header:   
```
"app_key: <<appId>
"Authorization:Bearer <<accessToken>> 
Content-Type:application/json;
```

Response TODO



## Push the data to your server
TODO
