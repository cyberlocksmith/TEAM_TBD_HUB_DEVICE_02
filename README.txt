README
==========================================================================
TEAM_TBD_sensors.py runs locally on the Hub Device. The modified .bashrc
file ensures that the program will start up when the device boots.
The .bashrc file will also start the Greengrass Core program with
device boot.

Setup Instructions: 
Start with a Raspberry Pi 3 that is set up with Raspbian OS and an
internet connection.
Unzip the Greengrass Core .tar.gz archive. Follow
installation instructions contained in the AWS Greengrass developer
guide (included in Reference PDFs).
Replace the .bashrc file in the Hub Device with the modified version,
and copy TEAMTBD_sensors.py into the /home/ directory.

Navigate to the AWS lambda console, making sure the region is the same
as was used in the Greengrass Core setup. Select "Create New Lambda
Function," and give it any name. Configure the code entry type as 
"Upload a .zip file." For the .zip file, select "team_tbd_function_01.zip"
Under Actions, select Publish New Version. Then, select Create New Alias.

On the IoT Core console, in the Greengrass Group created earlier, choose
"Lambdas" and then select "Add Lambda." Choose "Use Existing Lambda" to 
use the existing function code. Once done, click the three dots, select
"Edit Configuration," and change the timeout to 25 seconds and select
"Make this function long-lived and keep it running indefinitely."

Next add a subscription. Choose the source to be the Lambda function, 
and choose the destination to be IoT Core. The topic should be set to
"teamtbd/hub." 

If all setup was performed correctly, the Hub device should start to
log sensor events on startup. At this point, the messages should be viewable within 
the AWS MQTT client.
