# Add your first Device

![DeviceStep1](./images/DeviceStep1.png)

# Import Product
1. Download Product from GitHub Page  
https://github.com/alliot-at/Quickstart/blob/master/Product%20Profiles/tmaKeyValue_TMAKeyValue_V01.zip


![DeviceStep2](./images/DeviceStep2.png)  

1. Choose Product Model
2. Add Product Model
3. Import from Local
4. Enter: "GenericKeyValue" as Product Name
5. Choose downloaded file
6. Press "Confirm" 


![DeviceStep3](./images/DeviceStep3.png)  
1. Press "Confirm"  
   You don't have to save the secret

# Register your first Device

![DeviceStep4](./images/DeviceStep4.png)  
1. Open "Device" Menu
2. Choose "Registration"
3. Select "Single Registration"
4. Press "+ Register"

![DeviceStep5](./images/DeviceStep5.png)  
1.  Choose Product
2.  Select "GenericKeyValue"   
3.  Enter the IMEI of your module 
    The IMEI is printed on the module, or you can get it with the command:  `AT+CGSN=1` 
4.  Enter a Device Name
5.  Is Secure: No  **(only for testing)**  
    No - means that you can connect your module **with or without DTLS encryption**
6.  Region (e.g. Vienna)
7.  Set the correct Time zone
8.  Select "DefaultGroup"
9.  Register Type: Dynamic Password Mode 
10. Location Type : You can choose between "Latitude & Longitude" or "City &          Address"
11. Enter the Location
12. Press "Submit" to finish registration

![DeviceStep6](./images/DeviceStep6.png) 
If you want to connect your device with DTLS encryption, save the PSK now!
1. Press "Submit" 

## Next Step: Connect your device: {docsify-ignore}

* [Quectel BC66](./Quectel_BC66/03_Connect_device_to_IoT-Gateway.md)  
* [Quectel BC68](./Quectel_BC68/03_Connect_device_to_IoT-Gateway.md)  
* [Quectel BG96](./Quectel_BG96/Bearer_Selection.md) 					
* [SARA N211](./SARA_N211/03_Connect_device_to_IoT-Gateway.md) 	    
* [SARA R412](./SARA_R412/CAT-M_Network_Selection.md)					

