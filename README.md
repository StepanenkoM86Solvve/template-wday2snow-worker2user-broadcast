
# Mule Kick: Workday employee to ServiceNow ticket

+ [Use Case](#usecase)
+ [Run it!](#runit)
    * [Running on CloudHub](#runoncloudhub)
    	* [Deploying your Kick on CloudHub](#deployingyourkickoncloudhub)
    * [Running on premise](#runonopremise)
        * [Properties to be configured](#propertiestobeconfigured)
+ [Customize It!](#customizeit)
    * [config.xml](#configxml)
    * [inboundEndpoints.xml](#inboundendpointsxml)
    * [businessLogic.xml](#businesslogicxml)
    * [errorHandling.xml](#errorhandlingxml)
+ [Testing the Kick](#testingthekick)

# Use Case <a name="usecase"/>


# Run it! <a name="runit"/>

Simple steps to get Workday employee to ServiceNow ticket running 

## Running on CloudHub <a name="runoncloudhub"/>

While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to Deployment > Advanced to set all environment variables detailed in **Properties to be configured** as well as the **mule.env**. 

Once your app is all set and started, supposing you choose as domain name `Workday employee to ServiceNow ticket` to trigger the use case you just need to hit `http://Workday employee to ServiceNow ticket.cloudhub.io/synccontacts` and report will be sent to the emails configured.

### Deploying your Kick on CloudHub <a name="deployingyourkickoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Kick directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)


## Running on premise <a name="runonopremise"/>
Complete all properties in one of the property files, for example in [mule.prod.properties] (../blob/master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`.

After this, to trigger the use case you just need to hit the local http endpoint with the port you configured in your file. If this is, for instance, `9090` then you should hit: `http://localhost:9090/synccontacts` and this will create a CSV report and send it to the mails set.

## Properties to be configured (With examples)<a name="propertiestobeconfigured"/>
In order to use this Mule Kick you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detail list with examples:
...

# Customize It!<a name="customizeit"/>
This brief guide intends to give a high level idea of how this Kick is built and how you can change it according to your needs.
As mule applications are based on XML files, this page will be organised by describing all the XML that conform the Kick.
Of course more files will be found such as Test Classes and [Mule Application Files](http://www.mulesoft.org/documentation/display/current/Application+Format), but to keep it simple we will focus on the XMLs.

Here is a list of the main XML files you'll find in this application:

* [config.xml](#configxml)
* [inboundEndpoints.xml](#inboundendpointsxml)
* [businessLogic.xml](#businesslogicxml)
* [errorHandling.xml](#errorhandlingxml)


## config.xml<a name="configxml"/>
This file holds the configuration for Connectors and [Properties Place Holders](http://www.mulesoft.org/documentation/display/current/Configuring+Properties) are set in this file. 
**Even you can change the configuration here, all parameters that can be modified here are in properties file, and this is the recommended place to do it so.** 
Of course if you want to do core changes to the logic you will probably need to modify this file.

In the visual editor they can be found on the *Global Element* tab.


## indboundEndpoints.xml<a name="inbpundendpointsxml"/>
This is the file where you will found the inbound and outbound sides of your integration app.
It is intented to define the application API.
...

## businessLogic.xml<a name="businesslogicxml"/>
This file holds the functional aspect of the kick , directed by one flow responsible of conducting the business logic.
...


## errorHandling.xml<a name="errorhandlingxml"/>
This is the right place to handle how your integration will react depending on the different exceptions. 
This file holds a [Choice Exception Strategy](http://www.mulesoft.org/documentation/display/current/Choice+Exception+Strategy) that is referenced by the main flow in the business logic.
...


## Testing the Kick <a name="testingthekick"/>

You will notice that the Kick has been shipped with test.
These devidi them self into two categories:

+ Unit Tests
+ Integration Tests

You can run any of them by just doing right click on the class and clicking on run as Junit test.

Do bear in mind that you'll have to tell the test classes which property file to use.
For you convinience we have added a file mule.test.properties located in "src/test/resources".
In the run configurations of the test just make sure to add the following property:

+ -Dmule.env=test