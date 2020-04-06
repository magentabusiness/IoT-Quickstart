# Getting Started with EC21 and IoT-Gateway with MQTT

### Register Device in Ocean Connect with IMEI as nodeID and secret as a security. After registering the device, kindly note the device ID and device secret.
### Make sure your UE is connected to the network with private APN for IoT-Gateway.

## 1. MQTT Configuration

Server: 160.44.204.79 

Port: 8883  

MQTT_Client_ID: `{IMEI}_0_0_YYYYMMDDhh`  (use any Date)  

## 2. Password and Username configuration

Username: `{IMEI}`

Password:    <https://codebeautify.org/hmac-generator>  
             Algorithm: HmacSHA256  
             Key: `YYYYMMDDhh` -- same as in the MQTT_Client_ID  
             Plain or Cipher Text: `device secret from Ocean connect, after successfully device registration`  
             Result Hash-Value is the **Password!**


## 3. AT Commands for MQTT connection
```javascript
AT+QMTCFG="SSL",1,1,2       // SSL connection configuration
---> OK

AT+QMTOPEN=1,"160.44.204.79",8883   //IoT-Gateway Server IP and port 
---> OK
---> +QMTOPEN: 1,0

AT+QMTCONN=1,"{nodeID}_2_0_2020040520","{Username}","{Password}"
---> OK
---> +QMTCONN: 1,0,0
```
```javascript
AT+QMTPUB=1,0,0,0,"/huawei/v1/devices/{nodeID}/data/json"

 {
  "identifier": "123",
  "msgType": "deviceReq",
  "hasMore": 0,
  "data": [
    {
      "serviceId": "{serviceId}",
      "serviceData": {
        "{parameter_1_Name}": {parameter_1_Value},
        "{parameter_2_Name}": {parameter_2_Value}
        ...
        ...
        "{parameter_N_Name}": {parameter_N_Value}
      }
    }
   ]
  }
CTRL+Z

---> +QMTPUB: 2,0,0
```