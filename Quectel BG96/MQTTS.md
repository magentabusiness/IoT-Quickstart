
# Getting Started with BG96 and MQTTS

- [Getting Started with BG96 and MQTTS](#getting-started-with-bg96-and-mqtts)
    - [Create Device in Ocean Connect with Initial Password Mode](#create-device-in-ocean-connect-with-initial-password-mode)
    - [1. MQTT Configuration](#1-mqtt-configuration)
    - [2. Generate Password](#2-generate-password)
    - [3. TODO: Certificates (PEM Format)](#3-todo-certificates-pem-format)
    - [4. BG96 AT-Commands](#4-bg96-at-commands)

### Create Device in Ocean Connect with Initial Password Mode

### 1. MQTT Configuration
Server: 160.44.204.79   
Port: 8883  
MQTT_Client_ID: `{deviceId}`_0_0_YYYYMMDDhh  (use any Date)  
Username: `{deviceId}` 

### 2. Generate Password   
   https://codebeautify.org/hmac-generator  
   Algorithm: HmacSHA256  
   Key: `YYYYMMDDhh` -- same as in the MQTT_Client_ID  
   Plain or Cipher Text: `device secret from Ocean connect, after successfully device registration`   
   Result Hash-Value is the **Password!**

### 3. TODO: Certificates (PEM Format)  

### 4. BG96 AT-Commands
QCom Tool (included in Download here: https://www.quectel.com/Qdownload/BG96.html)

***Connect to Network***
```javascript
AT+CGDCONT=1,"IP","business.gprsinternet"
AT+QIACT=1
AT+QIACT?
```

***Upload Certificates to Module***  
Use the QCOM Tool to Send the Files
```javascript
AT+QFUPL="cacert.pem",{length}
AT+QFUPL="client.pem",{length}
AT+QFUPL="user_key.pem",{length}
```

***Configure SSL***
```javascript
AT+QMTCFG="SSL", 2,1,2
AT+QSSLCFG="cacert",2,"cacert.pem"
AT+QSSLCFG="clientcert",2,"client.pem"
AT+QSSLCFG="clientkey",2,"user_key.pem"
AT+QSSLCFG="seclevel",2,2
AT+QSSLCFG="sslversion",2,4
AT+QSSLCFG="ciphersuite",2,0xFFFF
AT+QSSLCFG="ignorelocaltime",2,1
```

***MQTT Connection***
```javascript
AT+QMTOPEN=2,"160.44.204.79",8883
Response:
+QMTOPEN: 2,0

AT+QMTCONN=2,"{MQTT_Client_ID}","{deviceId}","{password}"
Response:
+QMTCONN: 2,0,0

```

***Send Data (Report Data)***  
```javascript
AT+QMTPUB=2,0,0,0,"/huawei/v1/devices/{deviceId}/data/json"
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
Response:
+QMTPUB: 2,0,0
```

***Receive Data (Commands)***

Commands are sent via the Northound API.
`https://{{server}}/iocm/app/signaltrans/v1.1.0/devices/{{deviceId}}/services/IntData/sendCommand?appId={{appId}}`

```javascript 
AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/json",0 
Response
+QMTSUB: 2,1,0,0

AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary",0 

Response
+QMTSUB: 2,1,0,0

Receive:
+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary","{BinaryData}"

or
+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/json","{JsonData}"

```


