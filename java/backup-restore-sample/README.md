Backup & Restore sample
============================================

This sample demonstrates how one can backup the configuration file of a device in Cloudant NoSQL DB and restore the same later with a sample. The IBM Watson IoT Platform Events and Commands are used to backup and restore the configuration file. Refer to the [documentation](https://docs.internetofthings.ibmcloud.com/getting_started/concepts.html) to know more about the basic concepts like, Device, Application, Events, Commands and etc..

This recipe demonstrates the backup & restore of the configuration file using the following Events and Commands, 

* **backup-command** – A command that will be sent by the application to a device to backup the configuration file.
* **backup-event** – An event that will be sent by the device on receiving the backup-command, the event will have the contents of the configuration file.
* **restore-command** – A command that will be sent by the application to a device to restore the configuration file, the command will have the contents of the configuration file.
* **restore-ack** – An event that will be sent by the device after completing the restore operation, informing the status of the restore operation.

The above command and event names are just random names and can be replaced with any valid MQTT identifier.

----

### Tutorial Explaining the sample

Refer to [this recipe](https://developer.ibm.com/recipes/tutorials/backup-restore-device-configuration-in-ibm-iot-foundation-2/), that explains the sample present in this github project in detail.

### Prerequisites
To build and run the sample, you must have the following installed:

* [git](https://git-scm.com/)
* [maven](https://maven.apache.org/download.cgi)
* Java 7+

----

### Register Device in IBM Watson IoT Platform

Follow the steps in [this recipe](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/) to register your device in Watson IoT Platform if not registered already. And copy the registration details, like the following,

* Organization-ID = [Your Organization ID]
* Device-Type = [Your Device Type]
* Device-ID = [Your Device ID]
* Authentication-Method = token
* Authentication-Token = [Your Device Token]

We need these details to connect the device to IBM Watson IoT Platform.

----

### Build & Run the sample using Eclipse

You must have installed the [Eclipse Maven plugin](http://www.eclipse.org/m2e/), to import & run the samples in eclipse. Go to the next step, if you want to run manually.

* Clone the gateway-samples project using git clone as follows,

    `git clone https://github.com/ibm-messaging/iot-backup-restore-sample.git`
    
* Import the backup-restore-sample project into eclipse using the File->Import option in eclipse.

**Start device sample**

* Modify the **device.properties** file with the device registration details. 

* Build & Run the **BackupAndRestoreDeviceSample** by right clicking on the project and selecting "Run as" option.

* Observe that the device connects to the Watson IoT Platform and listens for the backup & restore command from the application.

** Start Application sample **

* Modify the **application.properties** file with your Organization's name, API-Key and Token.

* Build & run the Application sample **BackupAndRestoreApplicationSample** by right clicking on the project and selecting "Run as" option. You must provide the Cloudant DB username and password. Please refer to [this recipe](https://developer.ibm.com/recipes/tutorials/backup-restore-device-configuration-in-ibm-iot-foundation-2/) for more information about how to create Cloudant DB and run the sample.

* Observe that the application starts and provides the following command that the user can perform,
     
    backup     :: Sends a backup command to the list of device(s)
	restore id :: Sends a restore command along with the config file. Specify the ID that you received during the backup.

* Type **backup** in the console to backup the device configuration file into Cloudant DB.

* Type **restore <id>** to restore the old configuration into the device.

----

### Building the sample - Required if you want to run the sample outside of Eclipse

* Clone the gateway-samples project using git clone as follows,
   
    `git clone https://github.com/ibm-messaging/iot-backup-restore-sample.git`
    
* Navigate to the advanced-gateway-sample project, 

    `cd iot-backup-restore-sample\java\backup-restore-sample`
    
* Run the maven build as follows,

    `mvn clean package`
    
This will download the Java Client library for Watson IoT Platform (Currently its shipped as part of this sample, but soon it will be made available in maven central repository), download all required dependencies and starts the building process. Once built, the sample can be located in the target directory, for example, target\ibmiot-device-backup-restore-sample-0.0.1.jar.

----

### Running the Device Sample outside Eclipse

* Navigate to **target/classes** directory and Modify the **device.properties** file with the device registration details. 

* Build & Run the **BackupAndRestoreDeviceSample** by executing the following command,

    `mvn exec:java -Dexec.mainClass="com.ibm.iotf.sample.client.device.BackupAndRestoreDeviceSample"`

**Note:** If there is an Error, try extracting the ibmwiotp.jar present in target/classes directory to the same location and run again. Remember the jar must be extracted in the same location. 

* Observe that the device connects to the Watson IoT Platform and listens for the backup & restore command from the application.

----

### Running the Application Sample outside Eclipse

* Modify the **application.properties** file with your Organization's name, API-Key and Token.

* Start the Application sample **BackupAndRestoreApplicationSample** by executing the following command, You must provide the Cloudant DB username and password. Please refer to [this recipe](https://developer.ibm.com/recipes/tutorials/backup-restore-device-configuration-in-ibm-iot-foundation-2/) for more information about how to create Cloudant DB and run the sample.

    `mvn exec:java -Dexec.mainClass="com.ibm.iotf.sample.client.device.BackupAndRestoreDeviceSample" -Dexec.args="<username> <password>"` 

* Observe that the application starts and provides the following command that the user can perform,
     
    backup     :: Sends a backup command to the list of device(s)
	restore id :: Sends a restore command along with the config file. Specify the ID that you received during the backup.

* Type **backup** in the console to backup the device configuration file into Cloudant DB.

* Type **restore <id>** to restore the old configuration into the device.

----
