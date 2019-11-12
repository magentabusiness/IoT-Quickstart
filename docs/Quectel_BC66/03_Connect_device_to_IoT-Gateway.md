# Connect Quectel BC66 to IoT-Gateway

!> **Prerequisites**
 > * [Install Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)   
 > * [Download latest Drivers](https://www.exar.com/product/interface/uarts/usb-uarts/xr21v1412)
 
# Configure Device
1. Insert SIM Card
2. Mount antenna
3. Check if DIP-Switch (J302) is in position: MAIN UART TO USB
4. Connect it with USB to your PC
5. Install Drivers
6. Check in Device Manager the correct COM-Port (Ch A)  
   ![Step4](../images/BC66_Step1.png)
7. Open Putty  


# Configure Putty     

   ![Putty](../images/BC66_Putty_Step1.png)    
   1. Enter correct COM-Port
   2. Set Baud rate (Speed) to 115200
   3. Connection Type: Serial
   4. Enter "BC66" as name  
   5. Press save

   ![Putty](../images/BC66_Putty_Step2.png)    
   1. Select "Terminal"
   2. Local echo: Force On
   3. Local line editing: Force On
   4. Select "Session"  

   ![Putty](../images/BC66_Putty_Step3.png)    
   1. Press Save
   2. Double-Click to "BC66" to connect Putty to your BC66 Module  


# Check Connection  
  ![Putty](../images/BC66_Putty_Step4.png) 
  1. Press `PWR_Key` on the module  
  2. Enter `AT` to check module  
  3. Enter `ATI` to check module

# Prepare BC66 (Do it only once)
```
    **"Press the PWR_Key on the Module"**
     F1: 0000 0000
     V0: 0000 0000 [0001]
     00: 0006 000C
     01: 0000 0000
     U0: 0000 0001 [0000]
     T0: 0000 00B4
     Leaving the BROM

     AT                                      #check the module
     --> OK                                  
    
     ATI                                     # check the revision of the module, Currentely our IoT Gateway 
                                               supports BC66NBR01A06 or older firmware for this module.
     --> Quectel_Ltd
        Quectel_BC66
        Revision: BC66NBR01A06

        OK

     AT+QCGDEFCONT="IP","alliot.nbiot.at"    # Set APN
     --> OK 

     AT+QRST=1                               # Restart, will take 5 sec
     --> F1: 0000 0000
        V0: 0000 0000 [0001]
        00: 0006 000C
        01: 0000 0000
        U0: 0000 0001 [0000]
        T0: 0000 00B4
        Leaving the BROM    

     AT                                      # Auto baud synchronization
     --> OK

     AT+CFUN?                                # Radio Module Functionality 
     --> +CFUN : 1                           # 1 means fully functionality

     AT+QSCLK=0                              # See Notes at end of this document
     --> OK                            

     AT+QCGDEFCONT?                          # Check the APN
     --> +QCGDEFCONT: "IP","alliot.nbiot.at"

     AT+CGSN=1
     --> You will get your IMEI in response.

     // Configure the Ip and port of the IoT-Gateway
     AT+QLWCONFIG=0,10.112.28.10,5683,86***********77,900,3
     --> OK

     AT+QLWCFG="auto_reg",1                  # Auto register to the IoT Platform
     --> OK

     AT+CEREG=1                              # Enable network registration unsolicited 
     --> OK

     AT+CPSMS=0                              # Disable Power Saving Mode
     --> OK

     AT+CSCON=1                              # Enable Signalling Connection Status
     --> OK  
    
     --> +CSCON: 1                           # Connected Mode

     --> +CEREG: 5                           # Attached to Network

     --> +IP: 1*.*.*.***                     # IP Address
     
     --> +QLWURC: reg,0                      # Module registered to IoTGateway successfully

     --> +QLWOBSERVE: 0,19,0,0               # Module is ready to send Data
                      
```

##  Connect BC66 to NB-IoT Network and IoT-Gateway (Do it after each reboot, If you are not connected automatically to Network and Gateway)

``` 
        AT+QSCLK=0
        --> OK

        AT+CEREG=5
        --> OK

        AT+CSCON=1
       --> OK

       --> +CEREG: 5,"XXXX","XXXX",9,0,0,"XXXX","XXXX"

       --> +IP: 10.XX.XX.XX

       --> +QLWURC: reg,0

       --> +QLWOBSERVE: 0,19,0,0

 ```

    

**Once you receive the notification of successful registration and observe an object 19, after every reboot module will connect to the IoT-Gateway automatically.**

![After reboot](../images/BC66_Putty_Step5.png)

## Next Step: Send data from your Device to IoT-Gateway  / Link: [Send DATA](./Quectel_BC66/04_Send_Data_BC66.md) {docsify-ignore}

## Check Signal
```
AT+CESQ                             # Query the signal strength
--> +CESQ: 40,7,255,255,0,48

    OK

AT+QENG=0                           # Query the module status.
--> +QENG: 0,3547,2,127,"490A65",-91,-21,-70,1,8,"3AD6",0,230

    OK  
```  

## Check IP Address
``` 
AT+CGPADDR=1
-->  +CGPADDR:1,10.X.Y.Z

     OK
```

## Check IoT-Gateway  
* [Add your first device](./02_Add_first_Device.md)
* Check if your IMEI is correct.

NOTE : Quectel BC66 module switch off the UART interface for the power saving purpose. Therefor it may happen that Module accept the AT commands only when yyou enter same AT command two times. To avoid this, please excecute AT+QSCLK=0 after every reboot and power on.






