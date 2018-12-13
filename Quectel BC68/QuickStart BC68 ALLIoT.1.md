# Quick Start guide

## Quectel BC68

The Quectel BC68 module is controlled by AT Commands. These are ASCII commands that are sent to the module over the serial interface at 9600bps. If the command is executed correctly, the module replies with OK.

First, download and install the serial driver. https://www.exar.com/design-tools/software-drivers

You can write an embedded application on an embedded board like Arduino that communicates with the module, or you can send the commands directly from your computer over the serial interface. To do so you must connect the USB interface to the PC and use putty to send commands to the module.

Configuration of the Module and attach to network:

Interrogate Deviceinfo  
`ATI`

NCONFIG settings are saved into the memory of the module. You only need to do this once.  
`AT+NCONFIG="CR_0354_0338_SCRAMBLING","TRUE"`  
`AT+NCONFIG="CR_0859_SI_AVOID","FALSE"`

Configure to connect to ALLIoT  
`AT+NCDP=10.112.28.10,5683`

Reboot the Module  
`AT+NRB`

Switch the radio off by:  
`AT+CFUN=0`

Then set the APN for authentication  
`AT+CGDCONT=0,"IP","alliot.nbiot.at”`

Then switch on the radio. The previous commands are ‘sticky’ (stored in NVRAM) so only need to be entered once.  
Next time you can just start with this command:  
`AT+CFUN=1`

Then select the right band (in case of T-Mobile BAND 8)  
`AT+NBAND=8`

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
AT+QREGSWT=1            # Automatic registration mode (ALLIoT)
AT+CFUN=1               # Enable Radio Module
AT+CPSMS=1              # Enable Power Saving Mode
AT+NPSMR=1              # Enable Power Saving Mode Status Report
AT+COPS=1,2,"23203"    # Forces an attempt to select and register with the network operator (23203 is T-Mobile AT) wait for 30sek – 300sek 

### Responses from Modem

+CEREG:2      # Search for Network

+CSCON:1      # Connected Mode

+CEREG:5      # Attached to Network

+QLWEVTIND=0  # Registration on ALLIoT successful

+QLWEVTIND=3  # Ready to send Data
.
..

+CSCON:0      # Idle Mode


+NPSMR:1      # Power Saving Mode active

...
...

AT+QLWULDATA=......    # Send Data  - see "CIG-Codec.md"

``` 

