# Quick Start guide

## ublox SARA-N211

The SARA-N211 module is controlled by AT Commands. These are ASCII commands that are sent to the module over the serial interface at 9600bps. If the command is executed correctly, the module replies with OK.

Support and Infos: https://support.sodaq.com/sodaq-one/sara/
Setting up your Arduino IDE  http://support.sodaq.com/sodaq-one/arduino-ide-setup/

You can write an embedded application on the onboard Arduino that communicates with the module, or you can send the commands directly from your computer over the serial interface. 
To do so you must run the Demo "nbIOT_serial_passthrough" on the Arduino and connect the USB interface to the PC and use putty to send commands to the module.


Configuration of the Module and attach to network:

Interrogate Deviceinfo  
`ATI`

NCONFIG settings are saved into the memory of the module. You only need to do this once.  
`AT+NCONFIG="CR_0354_0338_SCRAMBLING","TRUE"`  
`AT+NCONFIG="CR_0859_SI_AVOID","FALSE"`

Configure to connect to ALLIoT  
`AT+NCDP="10.112.28.10",5683`

Reboot the Module  
`AT+NRB`

Switch the radio off by:  
`AT+CFUN=0`


Then switch on the radio. The previous commands are ‘sticky’ (stored in NVRAM) so only need to be entered once.  
Next time you can just start with this command:  
`AT+CFUN=1`

Then set the APN for authentication  
`AT+CGDCONT=0,"IP","alliot.nbiot.at"`

Forces an attempt to select and register with the network operator (23203 is T-Mobile AT) wait for 30sek – 300sek  
`AT+COPS=1,2,"23203"`

You can now check the signal quality. Keep repeating this until you get something else than 99,99.  
`AT+CSQ`

You can now check if you are attached to the network. If you get a value of 1 you are!  
`AT+CGATT?`

You can check your IP address. This is from a private IP range.  
`AT+CGPADDR`
 
Here are some more commands:  

Check the manufacturer of the module:  
`AT+CGMM`

Check the firmware version:  
`AT+CGMR`

Check the IMEI Number:  
`AT+CGSN=1`

Display network statistics. If you contact our support, check always the output of this command!  
`AT+NUESTATS` 


## Init Commands
```
AT+NRB                  # Reboot 
AT+CEREG=1              # Enable network registration unsolicited result code: “+CEREG:<stat>”
AT+CSCON=1              # Enagle Signalling Connection Status
AT+CFUN=1               # Enable Radio Module
AT+CGDCONT=0,"IP","alliot.nbiot.at"  # Set APN
AT+CPSMS=1              # Enable Power Saving Mode
AT+NPSMR=1              # Enable Power Saving Mode Status Report
AT+COPS=1,2,"23203"     # Forces an attempt to select and register with the network operator (23203 is T-Mobile AT) wait for 30sek – 300sek 

### Responses from Modem

+CEREG:2      # Search for Network

+CSCON:1      # Connected Mode

+CEREG:5      # Attached to Network
.
..

+CSCON:0      # Idle Mode


+NPSMR:1      # Power Saving Mode active

...
...

AT+NMGS=....  # Send Data  - see CIG-Codec description

+NPSMR:0      # deactivate Power Saving Mode

+CSCON:1      # Connected Mode

``` 

continue with "CIG-Codec" and send some Data

