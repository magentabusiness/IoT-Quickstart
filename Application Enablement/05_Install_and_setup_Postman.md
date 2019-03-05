# Quickstart - Application Enablement with Postman

- [Quickstart - Application Enablement with Postman](#quickstart---application-enablement-with-postman)
  - [Install Postman](#install-postman)
  - [Configure Postman](#configure-postman)
  - [Import Demo Certificate](#import-demo-certificate)
  - [Import Examples](#import-examples)
  - [Import and Configure Postman Environment](#import-and-configure-postman-environment)
    - [Import IoT-Gateway Environment](#import-iot-gateway-environment)
    - [Configure IoT-Gateway Environment](#configure-iot-gateway-environment)
  - [Next Step: Connect to the Rest API](#next-step-connect-to-the-rest-api)
  - [Troubleshooting](#troubleshooting)

## Install Postman

Download and install Postman on your PC   
https://www.getpostman.com/

## Configure Postman
![Postman SSL](../images/Postman_settings_ssl.png)
Open Settings  
1. Click Settings Icon
2. Select Settings
3. SSL Verification off 
4. Choose Certificates for the next step
   


## Import Demo Certificate
 
**IMPORTANT: You may only use this client Certificate only for testing.**  
**For production use, you have to request your own client certificate from T-Mobile Austria.**

* Download (Save Link to PC): [Demo Certificate](https://raw.githubusercontent.com/alliot-at/Quickstart/master/Application%20Enablement/Demo_Client_Certificates/IoT-Gateway.crt)
* Download (Save Link to PC): [Demo Certificate Key](https://raw.githubusercontent.com/alliot-at/Quickstart/master/Application%20Enablement/Demo_Client_Certificates/IoT-Gateway.key)



![Postman Client Certificate](../images/Postman_settings_certificate.png)

1. Host: 160.44.201.125
2. Port: 8743
3. CRT File --> choose "IoT-Gateway.crt" 
4. Key File --> choose "IoT-Gateway.key" 
5. Password: alliot
6. Click Add

## Import Examples

* Download Examples (Save Link to PC): 
  [IoT-Gateway Examples](https://raw.githubusercontent.com/alliot-at/Quickstart/master/Application%20Enablement/IoT-Gateway_Demos.postman_collection.json)  
Import in Postman
1. File -> Import  
2. Import File  
![Postman Import](../images/Postman_import.png)  
Choose File IoT-Gateway_Demos.postman_collection.json
3. After import   
![Postman Import](../images/Postman_import_ok.png)   

## Import and Configure Postman Environment

Environments

An environment is a set of key-value pairs. The key represents the name of the variable. You can use a data editor to modify an environment.

While working with APIs, you often need different setups for your local machine, the development server, or the production API. Environments let you customize requests using variables so you can easily switch between different setups without changing your requests.

You won’t have to remember all those values once they are in Postman. You can download environments, save them as JSON files, and upload them later.

You can create, share, duplicate, export, and delete an environment. You can also import an environment as a single JSON file. 

Further informations: https://learning.getpostman.com/docs/postman/environments_and_globals/manage_environments/

### Import IoT-Gateway Environment

* Download Examples (Save Link to PC):
  [IoT-Gateway Environment](https://raw.githubusercontent.com/alliot-at/Quickstart/master/Application%20Enablement/IoT-Gateway_Demo.postman_environment.json)  

![Postman Manage Environments](../images/Postman_manage_environment.png)
1. Click "Manage Environments"
2. Click "Import"
3. Choose "IoT-Gateway_Demo.postman_environment.json"

### Configure IoT-Gateway Environment

Open Environment<br>   
![Postman Manage Environments](../images/Postman_environment.png)
1. Choose "IoT-Gateway Demo" 
2. Click "Environment quick look"
3. Click "Edit"

Configure the Environment for your Application and Device<br>   
Now you need your Application Credentials, which you have downloaded in the first Part of the Tutorial ( [Create your first Application](../01&#32;Create&#32;first&#32;Application.md) )  (Step: Save Secert to Local)  
So open the File and get your AppID and AppSecret

![Postman Manage Environments](../images/Postman_environment_edit.png)
1. Enter your AppId
2. Enter your App Secret

## Next Step: [Connect to the Rest API](06_Connect_to_REST_API.md)


## Troubleshooting

If you have lost your AppSecret you can reset it, to get a new one. 
But then the old secret will not work anymore.
1. Open IoT-Gateway
2. Got to "System Manage" and choose your App
Click Reset to get a new AppSecret.





 
  
