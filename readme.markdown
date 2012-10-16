NServiceBus and SignalR
======================================================================
## Background
Having the distributed possibilities with NServiceBus in an event driven architecture and not taking it further to the client in a web application is not really doing it all the way. We know that we can rely on NServiceBus and SignalR is maturing every day. I felt it was time to sort things out regarding NServiceBus and SignalR and how they interact. And to provide an example as well.

## Points of interest
This is a really simple sample and no detail has gone into any of the parts. The purpose to provide easy understanding of configuration of the two frameworks and the interactions between them.

### Web Application
This is a ASP.NET MVC 4 Web Site from the basic template. The Web App has a simple page where three scenarios are demonstrated:
#### Hub
This is a standard Hub in SignalR. What I do in one browser gets sent to all the others (in this case). There's nothing special with this case.
#### Outside the Hub
This scenario is used when code outside of the Hub want to make use of the Hub connection and call methods on the client. This is our first step towards letting an NServiceBus handler calling clients.
#### NServiceBus handler using Hub
This scenario completes the circle. There are two ways to send messages. The first sends messages to the Console App where they are diplayed. The console app can also send messages to the client. It's like a chat. The second way is a loopback mechanism where the web sends a message to itself. This is in case you don't want to use the Console App at all.

Added packages:
	* NServiceBus 3.2.8
	* SignalR 0.5.3
	* jQuery 1.8.2

### ConsoleApp
This is a very simple Console Application. The purpose is just to show that it is possible to send messages from a separate (server) process  to the client (GUI even).

Added packages:
	* NServiceBus 3.2.8
	
## Installation

You should be able to just fork the project and rum the solution. But here are some things off the top of my head:
	* If you haven't run NServiceBus on the machine before, go to [NServiceBus.com](http://nservicebus.com/Downloads.aspx) and download it and then run the 'runmefirst.bat' from the package. It will setup Message Queueing and the DTC and some other magical things. Don't forget to unblock the file before unxipping it.
	* The message queues are supposed to be created automatically, but NServiceBus might have a bad day (in terms of permissions) and fail to install them. The queues you need are (oh, and they are transactional):
		* NServiceBusSignalR.Web
		* NServiceBusSignalR.Web.Retries
		* NServiceBusSignalR.ConsoleApp
		* NServiceBusSignalR.ConsoleApp.Retries
		* NServiceBusSignalR.Error
	* You should run SignalR on an IIS or an IIS Express or a late version. Like 7.5. 
	
### Coming up
I want to add dependency injection to this as that is what I use myself and if I can isolate the interactions in a similar manner, I think I can learn some from that as well. 

### Questions, Thoughts?
Contact me on twitter [@MikaelOstberg](https://twitter.com/mikaelostberg)
		