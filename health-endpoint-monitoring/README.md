# Health Endpoint Monitoring Pattern

This document describes the Health Endpoint Monitoring Pattern example from the guide [Cloud Design Patterns](http://aka.ms/Cloud-Design-Patterns).

## System Requirements

* Microsoft .NET Framework version 4.5
* Microsoft Visual Studio 2015 Comunity, Enterprise, or Professional
* Windows Azure SDK for .NET version 2.9

## Before you start

Ensure that you have installed all of the software prerequisites.

The example demonstrates operational aspects of applications running in Windows Azure. Therefore, you will need to use the diagnostics tools in order to understand how the code sample works. You **must** ensure that the web and worker roles in the solution are configured to use the diagnostics mechanism. If not, you will not see the trace information generated by the example.

## About the Example
 
This example shows how you can set up a web endpoint that checks the health of dependent services by returning appropriate status codes. The endpoints are designed to be consumed by a watchdog monitoring service such as Windows Azure Endpoint Monitoring, but you can open and invoke the endpoint operations from a browser to see the results. You can also deploy and configure your own endpoint monitoring tool of choice to send requests to the service operations and analyze the responses received.


## Running the Example

You can run this example locally in the Visual Studio Windows Azure emulator. You can also run this example by deploying it to a Windows Azure Cloud Service.

* Start Visual Studio using an account that has Administrator privileges ("Run as Administrator").
* Open the solution you want to explore from the subfolders where you downloaded the examples.
* Right-click on each role in Solution Explorer, select Properties, and ensure that the role is configured to generate diagnostic information.

* If you want to run the example in the local Windows Azure emulator:
	* Press F5 in Visual Studio to start the example running. 
	* Open the Windows Azure Compute Emulator UI from the icon in the notification area.
	* Select each role in turn and view the diagnostic information generated by Trace statements in the code.

* If you want to run the example on Windows Azure:
	* Provision a Windows Azure Cloud Service and deploy the application to it from Visual Studio. 
	* Open the Server Explorer Window in Visual Studio and expand the Windows Azure entry.
	* Expand Cloud Services and then expand the entry for the solution you deployed.
	* Right-click each role instance and select View Diagnostics Data to see the diagnostic information generated by Trace statements in the code. This is written to the WADLogsTable in the Storage/Development/Tables section.

* Navigate to one of the monitoring endpoints. Use the F12 Developer Tools in Internet Explorer or the equivalent in your browser to watch the network traffic response pattern. The response will be 200 (OK), or a 500 error code that indicates a problem with a service.
* The sample contains four endpoints that you can test:

	* **/HealthCheck/CoreServices** This is a simple check on dependent services to determine if they are responding.
	* **/HealthCheck/ObscurePath/{path}** This demonstrates a check operation that uses a configurable obscure path defined in the service configuration file. Replace path with the value of the setting named Test.ObscurePathfrom in the file ServiceConfiguration.*.csfg. Note that this technique is not to be used as an alternative to properly securing an application and implementing authentication.
	* **/HealthCheck/CheckUnstableServiceHealth** This will randomly return a 500 exception for approximately 20% of the requests.
	* **/HealthCheck/TestResponseFromConfig** This returns a response code set in configuration (.cscfg) for testing. Deploy the solution with endpoint monitoring configured to use this operation, and then explicitly set the "Test.ReturnStatusCode" setting to return the required status code to test and demonstrate the effects of these codes on the monitoring service.




