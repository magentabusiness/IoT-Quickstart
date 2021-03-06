
# Device Capability Profile Development Guide

## Device profile naming rules

- Device types, service types and serviceIDs must start with in **capital**.
- Attribute or service name, uncapitalise the first word and capitalise first letter of the second word.
- A device capability profile file name must be **"devicetype-capability.json"**
- A service capability profile file name must be      **"servicetype-capability.json"**
- Static information (manufacture ID, manufacture name and device model) in device model must be unique.
- Universal service capabilities (Battery, Connectivity, Location, Modem Battery) are already defined and should be same for every device model.

Detail described device model example shown below. This device model is for temperature and clock with typical universal services.

Hint : Every files will be in **.json** format. Once you finish entering the JSON fields, try to check the validity of the JSON by using some websites.

### Optional: Download Example

To speedup your development- you can also download or clone the example Product Model:
[GitHub: DemoSensor_MagentaIoT_V001](https://github.com/magentabusiness/DemoSensor_MagentaIoT_V001)

## Step 1: Writing **"devicetype-capability.json"** file for General device

A devicetype-capability.json file include the static information about the device and the services along with om capabilities (FOTA, SOTA).

1. Create new folder named **"profile"**. (Name **must** be the same.)
2. Inside the **"profile"** folder, create the json file named **devicetype-capability.json** with using text editor. [If you using Notepad ++, File -> New]
3. Add this json code with mandatory field.

   - **manufactureId, manufactureName** should not contains any space or spacial character such as "_ , -, /".
   - **manufactureId, manufactureName, model** must be unique, You will need it at the time of Upload product to the IoT-Gateway.

   ```xml
   {
      "devices": [
            {
                "manufacturerId": "MagentaIoT",
                "manufacturerName": "Magenta_IoT",
                "model": "V001",
                "protocolType": "LWM2M",
                "deviceType": "DemoSensor",
                "omCapabilitiy": **....**
                "serviceTypeCapabilities": **....**
            }
        ]
    }
    ```

4. Add this json **in the field** of omCapability.

    ```json
    "omCapability":{
            "upgradeCapability" : {
                    "supportUpgrade":false,
                    "upgradeProtocolType":"PCP"
                        },
            "fwUpgradeCapability" : {
                    "supportUpgrade":true,
                    "upgradeProtocolType":"LWM2M"
                        }
                }
    ```

5. Add services **in the field** of serviceTypeCapabilities according to your device. ( In this test model we described with the universal services. )

     ```json
    "serviceTypeCapabilities": [
        {
          "serviceId": "Battery",
          "serviceType": "Battery",
          "option": ""
        },
        {
          "serviceId": "Connectivity",
          "serviceType": "Connectivity",
          "option": ""
        },
        {
          "serviceId": "Location",
          "serviceType": "Location",
          "option": ""
        },
        {
          "serviceId": "Temperature",
          "serviceType": "Temperature",
          "option": "Mandatory"
        },
        {
          "serviceId": "Clock",
          "serviceType": "Clock",
          "option": "Mandatory"
        }
      ]
    ```

6. After adding the om capability and services, device-capability.json   will look like

     ```json
     {
     "devices": [
    {
      "manufacturerId": "MagentaIoT",
      "manufacturerName": "Magenta_IoT",
      "model": "V001",
      "protocolType": "LWM2M",
      "deviceType": "DemoSensor",
      "omCapability":{
            "upgradeCapability" : {
                    "supportUpgrade":true,
                    "upgradeProtocolType":"PCP"
                        },
            "fwUpgradeCapability" : {
                    "supportUpgrade":true,
                    "upgradeProtocolType":"LWM2M"
                        }
                },
      "serviceTypeCapabilities": [
               {
                  "serviceId": "Battery",
                  "serviceType": "Battery",
                  "option": "Mandatory"
                },
                {
                  "serviceId": "Connectivity",
                  "serviceType": "Connectivity",
                  "option": "Mandatory"
                },
                {
                  "serviceId": "Location",
                  "serviceType": "Location",
                  "option": "Mandatory"
                },
                {
                  "serviceId": "Temperature",
                  "serviceType": "Temperature",
                  "option": "Mandatory"
                },
                {
                  "serviceId": "Clock",
                  "serviceType": "Clock",
                  "option": "Mandatory"
             }
           ]
         }
       ]
     }
    ```

7. Save this file. Later we will need it for packing the profile.

## Step 2 : Writing **"servicetype-capability.json"** file for General device

1. Create the new folder named **"service"**. (Name **must** be the same.)

2. Inside the **"service"** folder, create folders according to your services. As we are creating device with the services (Battery (01), Connectivity (02), Location (03), Temperature(04), Clock(05)), **Create five new folder with the same name as your serviceType**.

3. Inside the **Battery** folder, create a new folder named **profile**. create **"servicetype-capability.json"** file inside the **profile** folder and add this json code.

     ```json
     {
       "services": [
        {
             "serviceType": "Battery",
             "description": "",
             "commands": [],
             "properties": [
             {
                 "propertyName": "batteryLevel",
                  "dataType": "int",
                  "required": true,
                  "min": "0",
                  "max": "100",
                  "step": 1,
                  "maxLength": 0,
                  "method": "R",
                  "unit": "%",
                  "enumList": null
              },
              {
                "propertyName": "batteryVoltage",
                  "dataType": "int",
                  "required": true,
                  "min": "0",
                  "max": "10000",
                  "step": 1,
                  "maxLength": 0,
                  "method": "R",
                  "unit": "mV",
                  "enumList": null
             }
            ],
            "events": []
         }
       ]
     }
     ```

4. Inside the **Connectivity** folder, create a new folder named **profile**. create **"servicetype-capability.json"** file inside the **profile** folder and add this json code.

     ```json
     {
    "services": [{
        "serviceType": "Connectivity",
        "description": "",
        "commands": [],
        "properties": [{
                "propertyName": "rsrp",
                "dataType": "decimal",
                "required": true,
                "min": -5000,
                "max": 5000,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": "dBm",
                "enumList": null
            },
            {
                "propertyName": "rsrq",
                "dataType": "decimal",
                "required": false,
                "min": -500,
                "max": 500,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": null,
                "enumList": null
            },
            {
                "propertyName": "cellId",
                "dataType": "int",
                "required": false,
                "min": 0,
                "max": 268435455,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": null,
                "enumList": null
            },
            {
                "propertyName": "rssi",
                "dataType": "decimal",
                "required": false,
                "min": 0,
                "max": 310,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": null,
                "enumList": null
            },
            {
                "propertyName": "celevel",
                "dataType": "int",
                "required": false,
                "min": 0,
                "max": 2,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": null,
                "enumList": null
            },
            {
                "propertyName": "sinr",
                "dataType": "decimal",
                "required": false,
                "min": -200,
                "max": 300,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": "dB",
                "enumList": null
            },
            {
                "propertyName": "snr",
                "dataType": "decimal",
                "required": false,
                "min": -200,
                "max": 300,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": "dB",
                "enumList": null
            },
            {
                "propertyName": "pci",
                "dataType": "int",
                "required": false,
                "min": null,
                "max": null,
                "step": null,
                "maxLength": null,
                "method": "RE",
                "unit": null,
                "enumList": null
            }
        ],
        "events": []
         }]
     }
     ```

5. Inside the **Location** folder, create a new folder named **profile**. create **"servicetype-capability.json"** file inside the **profile** folder and add this json code.

     ```json
     {
       "services": [
        {
      "serviceType": "Location",
      "description": "",
      "commands": [],
      "properties": [
        {
          "propertyName": "longitude",
          "dataType": "decimal",
          "required": true,
          "min": "-180",
          "max": "180",
          "step": 1,
          "maxLength": 0,
          "method": "RWE",
          "unit": "°",
          "enumList": null
        },
        {
          "propertyName": "latitude",
          "dataType": "decimal",
          "required": true,
          "min": "-90",
          "max": "90",
          "step": 1,
          "maxLength": 0,
          "method": "RWE",
          "unit": "°",
          "enumList": null
        }
      ],
      "events": []
     }
       ]
     }
     ```

6. Inside the **Temperature** folder, create a new folder named          **profile**. create **"servicetype-capability.json"** file inside the     **profile** folder and add this json code.
    - Here in this service, we will add few commands and response.

     ```json
     {
          "services": [
    {
      "serviceType": "Temperature",
      "description": "",
      "commands": [
        {
           "commandName": "SET_MEASURE_PERIOD",
           "paras": [
               {
                   "paraName": "value",
                   "dataType": "int",
                   "required": true,
                   "min": 1,
                   "max": 1000,
                   "step": 1,
                   "maxLength": 10,
                   "unit": "minute",
                   "enumList": null
                 }
         ],
            "responses": [
               {
                   "responseName": "SET_MEASURE_PERIOD_RSP",
                   "paras": [
                      {
                             "paraName": "result",
                             "dataType": "int",
                             "required": true,
                             "min": -1000000,
                             "max": 1000000,
                             "step": 1,
                             "maxLength": 10,
                             "unit": null,
                             "enumList": null
                       }
                   ]
               }
           ]
        },
        {
           "commandName": "SET_TRANSFER_PERIOD",
           "paras": [
               {
                   "paraName": "value",
                   "dataType": "int",
                   "required": true,
                   "min": 1,
                   "max": 1000,
                   "step": 1,
                   "maxLength": 10,
                   "unit": "minute",
                   "enumList": null
                 }
         ],
            "responses": [
               {
                   "responseName": "SET_TRANSFER_PERIOD_RSP",
                   "paras": [
                      {
                             "paraName": "result",
                             "dataType": "int",
                             "required": true,
                             "min": -1000000,
                             "max": 1000000,
                             "step": 1,
                             "maxLength": 10,
                             "unit": null,
                             "enumList": null
                       }
                   ]
               }
           ]
        }
      ],
      "properties": [
        {
          "propertyName": "temperature",
          "dataType": "decimal",
          "required": true,
          "min": "0",
          "max": "100",
          "step": 1,
          "maxLength": 0,
          "method": "RWE",
          "unit": "C",
          "enumList": null
        }
      ],
      "events": []
     }
     ]
     }
     ```

7. Inside the **Clock** folder, create a new folder named **profile**. create **"servicetype-capability.json"** file inside the **profile** folder and add this json code.

     ```json
      {
     "services": [
    {
      "serviceType": "Clock",
      "description": "",
      "commands": [],
      "properties": [
        {
          "propertyName": "timeRequest",
          "dataType": "int",
          "required": true,
          "min": "0",
          "max": "100",
          "step": 1,
          "maxLength": 0,
          "method": "RWE",
          "unit": "",
          "enumList": null
        }
      ],
    "events": []
      }
     ]
    }
     ```

## Step 3: Packing the profile for the IoT Gateway

### General hierarchy of device profile

  The general file folder hierarchy should be look like this. **The Names which are written in red fonts are case sensitive and your profile should have same name.**

  1) Compressed the **profile** folder and **service** folder in .zip format.
  2) Our Device is ready for IoT Gateway.
  3) Device model what we developed, should be look like this after the .zip compression.

  ![General Hierarchy](../images/Device_Profile.png)

## Step 4: Import Product Model  

[Import Product Model.](02_Add_first_Device.md#import-product)
