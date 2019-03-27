
# CIG Plugin Development  (coming soon.. - documentation not finished)
- [CIG Plugin Development (coming soon.. - documentation not finished)](#cig-plugin-development-coming-soon---documentation-not-finished)
  - [Prepare Development Environment](#prepare-development-environment)
    - [Configure Maven Plugin:](#configure-maven-plugin)
  - [Import example CIG Plugin](#import-example-cig-plugin)
  - [Customize for your Product Model](#customize-for-your-product-model)
  - [Build CIG Plugin](#build-cig-plugin)
  - [Test CIG Plugin](#test-cig-plugin)


## Prepare Development Environment  
1. Download and extract Eclipse: https://www.eclipse.org/downloads/   
  [Installation Help ](https://wiki.eclipse.org/Eclipse/Installation)
2. Download an install Maven: http://maven.apache.org/download.cgi  (Binary zip archive)
### Configure Maven Plugin:  
1. Start Eclipse and choose Windows > Preferences. 
2. In the Preferences window, choose Maven > Installations. 
3. On the right pane, click Add.  
4. Select the directory, where you have unzipped maven - then click Finish.
5. Select the imported Maven plugin and click OK.

## Import example CIG Plugin
This CIG Plugin works with the Product Profile which is described here: 
[Device_Product_Profile_Development_Offline](Device_Product_Profile_Development_Offline.md)  
For Testing you can compile and test it, without any modifications.  
How to prepare it for your Product Profile is described below.

1. Download the example CIG-Plugin and unzip it. [LINK](../)
2. Open Eclipse and Import existing maven project
3. File > Import > Maven > Existing Maven Projects > Next
4. Choose the folder where you have unzipped the CIG-Plugin
5. Select pom.xml in the Projects-List.  
6. Click Finish. 

If you just want to test the plugin goto [Build CIG Plugin](#build-cig-plugin)


## Customize for your Product Model

1. Rename Project in Eclipse to `deviceType-manufacturerId-model` depending on your Product Profile. In our example it would be:  
deviceType: TestDevice  
manufacturerName: IoT_Company  
manufacturerId: IotCompany  
model: NBIoTDevice  
So the Project name is: `TestDevice-IoTCompany-NBIoTDevice`
2. Rename src/main/java Package Names to: `com.manufacturerName.model.deviceType`  
So the Package Name is: `com.IoT_Company.NBIoTDevice.TestDevice`   
**Enable Rename subpackages**
3. Rename src/test/java Package Names to: `com.manufacturerName.model.deviceType.Test`  
So the Package Name is: `com.IoT_Company.NBIoTDevice.TestDevice.Test`   
**Enable Rename subpackages**  
4. Update pom.xml  
Line 7: `<groupId>com.manufacturerName.model.deviceType</groupId>` (com.IoT_Company.NBIoTDevice.TestDevice)  
Line 9:  `<artifactId>deviceType-manufacturerId-model</artifactId>` (TestDevice-IoTCompany-NBIoTDevice)  
Line 84: `<Bundle-SymbolicName>deviceType-manufacturerId-model</Bundle-SymbolicName>` (TestDevice-IoTCompany-NBIoTDevice)
5. Update `/src/main/resources/OSGI-INF/CodecProvideHandler.xml`    
Update properties with ###
```xml
<?xml version="1.0" encoding="UTF-8"?>
<scr:component xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0" immediate="true" name="###com.manufacturerName.model.deviceType###.ProtocolAdapterImpl">
    <implementation class="###com.manufacturerName.model.deviceType###.ProtocolAdapterImpl"/>
    <service>
		<provide interface="com.huawei.m2m.cig.tup.modules.protocol_adapter.IProtocolAdapter" />
	</service>
</scr:component>
```
Example:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<scr:component xmlns:scr="http://www.osgi.org/xmlns/scr/v1.1.0" immediate="true" name="com.IoT_Company.NBIoTDevice.TestDevice.ProtocolAdapterImpl">
    <implementation class="com.IoT_Company.NBIoTDevice.TestDevice.ProtocolAdapterImpl"/>
    <service>
		<provide interface="com.huawei.m2m.cig.tup.modules.protocol_adapter.IProtocolAdapter" />
	</service>
</scr:component>
```
6. Update `/target/package/package-info.json`   
Update properties with ###
```json
{
    "specVersion":"1.0",
    "fileName":"###deviceType-manufacturerId-model###",
    "version":"1.0.0",
    "deviceType":"###deviceType###",
    "manufacturerName":"###manufacturerId###",
    "model":"###model###",
    "description":"codec",
    "platform":"linux",
    "packageType":"CIGPlugin",
    "date":"2019-03-06 12:16:59",
	"ignoreList":[],
    "bundles":[
    {
        "bundleName": "###deviceType-manufacturerId-model###",
        "bundleVersion": "1.0.0",
        "priority":5,
        "fileName": "###deviceType-manufacturerId-model###-1.0.0.jar",
        "bundleDesc":"",
        "versionDesc":""
    }]
}
```

Example:
```json
{
    "specVersion":"1.0",
    "fileName":"TestDevice-IoTCompany-NBIoTDevice",
    "version":"1.0.0",
    "deviceType":"TestDevice",
    "manufacturerName":"IoTCompany",
    "model":"NBIoTDevice",
    "description":"codec",
    "platform":"linux",
    "packageType":"CIGPlugin",
    "date":"2017-02-06 12:16:59",
	"ignoreList":[],
    "bundles":[
    {
        "bundleName": "TestDevice-IoTCompany-NBIoTDevice",
        "bundleVersion": "1.0.0",
        "priority":5,
        "fileName": "TestDevice-IoTCompany-NBIoTDevice-1.0.0.jar",
        "bundleDesc":"",
        "versionDesc":""
    }]
}
```

## Build CIG Plugin 

1. Open Command-Line and goto you Project Folder where the pom.xml is located.
2. Execute `mvn package`
3. If "BUILD SUCCESS" is displayed, the compiled package is located in the `target` folder.
4. The plugin is automatically zipped to `package.zip` - use this file to test the plugin.


## Test CIG Plugin

1. Download the [NB-IoT Encoding and Decoding Plugin Validation Tool](https://devcenter.huawei.com/ict/en/resource/tool)
2. Unzip the downloaded file
3. Copy your `devicetype-capability.json` from the Product Profile and the `package.zip` from the target Folder of your CIG Plugin into the same folder where `pluginDetector.jar` is located. 
4. Start `pluginDetector.jar`

next Step: Modify the CIG Plugin


 