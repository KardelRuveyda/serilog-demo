# serilog-demo
## Serilog Demo Application with Seq visualization

Hello everyone,

In the ever-evolving world of software development, one tool has made a significant mark - Serilog. But is it truly an elephant in the room, never forgetting the critical details of your application's life? In this exploration, we'll dive into the capabilities and qualities of Serilog to determine if its memory surpasses even that of the proverbial elephant. Actually, I will prepare presentation about Serilog in Dogus Technology's chapter Software Competency, so i decided writing this article. I will step by step explain my notes about Logging,Serilog etc. I hope, you are like . Thank you for reading.
Lets get started!

### What is Logging?
If you ask me, one of the most important structures in an application is logging. Logging records behaviour during the critical period when the application is in the live environment. Logs are a system that we use to make it easier for us to manage the problems experienced by the application at runtime.Logging is very important for problem solving.
In short, it is a mechanism that informs about the general behaviour of the application in processes with users. In addition, security policies can also be observed with logs.

### What details does the log mechanism contain?

**If you want to create log mechanism, you should answer below questions.**
- Who uses the system?
There should be information about which user caused the log to be created.
- Where did the error occur in the code?
The line and method in the code where the error occurred must be recorded.
- What is the error code?
The error code must be logged in the logging mechanism so that you can easily find out why this code failed.
- When did the error happen?
Time and date information should be kept in detail.
- Why did the application fail?
Detail should be kept as to why the error was received. In this way, the solution is more easily realised.

### What should be recorded in the log mechanism?
- Exceptions
It is necessary to record all information about the errors received. With this data I can find a solution to the error.
- Data Changes
You may not keep simple update operations in logging, but critical operations such as critical data, configurations should be kept in the system.
- Suspicious Activities
Continuous authentication requests to the application, access to restricted data, invalid parameters must be recorded.
- Requests
All requests from the user should be recorded in the log mechanism. Especially the date and time should be recorded in the request processes.
- User Information
The information of authenticated users must be saved.
- Summary Information
You can save the log with summary information. This is not necessary, but if you save it, this can be good for readability.

### What should not be recorded in the log mechanism?
- Sensitive Datas
You must not save sensitive data in the log mechanism. (User password,User Identity No, Secret Keys etc.)

### You may not prefer do this, i will give just logging extras
- Customising Error Messages
- Log records can be visualised ( For Example : Seq.)
### Where and how should records be kept?
- Console
You can print the logs on the console, but it may not be meaningful when you want to analyse.
**Logs must be physically stored in external files or databases in order to be analysed.**

### What is Serilog?
Serilog is a dotnet library that provides diagnostic logging to flies the console and almost everywhere you would like. Serilog can be used in dotnet framework applications and for applications running on greatest .NET 6. I used Serilog with .NET 6 in my demo. You can prefer other versions. 
One of the biggest strengths of serilog is that it has been built with structured logging in mind. You can find more information on Serilog's website link.


Summarly;
- Open-source .NET Library
- Provides a rich logging experience
- Runs on .NET Framework
- Runs on .NET 6
- Supports structured loging

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/74a1c1c5-8dbf-416a-8a8c-59864291f15c)

### Why do I use Serilog?
Let me tell you my personal experience with it i used Serilog in a few applications with different logging requirements and i was always satisfied with the results. I can not speak much about performance because i don't work with large distributed ultra scalable applications but the performance was never an issue in my use cases. I like serilog simple integration into the .Net applications the ease of use how simple you can start and what more advanced features are available and can be used later in your journey.


Summarly;
- Satisfied with the results.
- Performance was great.
- Simple integrate into .Net apps.

  
### Let's create an application and integrate Serilog in Visual Studio 2022.
  
**We create a new project based on the .Net Core Web Api project template.**


![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/265581b4-4faf-42a0-afa4-4019fce69199)

**We choose Serilog Demo as the project name and nex dialogue page,.**

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/8e10a00b-3bff-4335-b9d7-d96426d25d32)

**We stick with the defaults and use .Net 6. We click on create and wait until Visual Studio generated the project for us.**


![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/5120c0d7-3192-4f56-9cd3-bb68b62282ba)

**Installing Serilog is simple first. We open the Nuget Package Manager and search for the Serilog.AspNetCore package and install the latest stable version. After a few seconds Serilog is installed.**

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/1e5c539f-f3f4-4920-a0ac-b7e2bc8c5b3f)

Next let's integrate Serilog into our application by registering it as a logging provider. I insert the code snippet that defines a new logger configuration. We configure the configuration to read the application configuration from the applcation builder. We also enrich Serilog with the log context. Next we clear all existing logging providers. The web application builder adds for example the console logging provider and we want to get rid of that last but not least we add Serilog to the logging providers for our application and provide the configured logger configuration object as its sole argument. We configured the logger to use the settings from the application configuration.

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/6b79b5ef-8203-4dba-b0c8-6bc11881cc93)

**Let's open the appsetting.json file and configure Serilog. I ınsert the sample configuration. Let's take a look at it first there using property where we define an array of log targets.In Serilog log targets are called Sinks. We configure an array with a single Sinks the Serilog.Sinks.File.**
-**Next, we can configure log levels and more importantly to write to section.In the write to section, we configure information for the file Sink. The Name property with the value file defines that the property provided in the orgs property will be used for file Sink. We configured a path where our log file
- should be written. The rolling interval property defines when a new file should be created and the output template defines the structre of the log output for each log statement.**


![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/a00ada6f-363f-4c91-90ad-a6b1b26370e6)

**Now that Serilog is configured. We open the Weather Forecast controller class and insert a log statement in the get method.**

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/fac11e9d-f7a1-46ff-aa5f-cdf6947be15b)

**Now, let's start the application. We use record to send a simple get request to the WeatherForecastController. Open the entry in the endpoints list and click on the try out button. We click the big blue execute button to send a request. We receive an array with weather data.**


![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/23fed1a2-bf2e-42bb-9059-2a00da37b1a8)

**However let's close the application and lok at the log files. We open the project directory and open the logs folder.**

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/158bba21-b63a-4fe3-a089-49e78170e6dc)

**The file name contains the prefix we configured in appsettings.json file and the part after the dash is the current day with the current configuration Serilog creates a seperate file for every day we collect all the log statements for any given day in its file.**

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/9812fdf7-6d64-41e1-898c-5f69802cca1d)

**Let's open the file and scroll through it. We can see a timestamp and our log statement that we added to the WeatherForecastController class.**


![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/45562844-e6b2-47c1-95d6-c879bd7dea99)

**Now that we learned about the basics of Serilog and integrated it into our application, let's look at the Provided Sinks.**

### Provded Sinks

As we can see there are things for popular cloud providers including Amazon Cloudwatch, Azure Analytics and many other cloud services. There are also Sinks for the window event log Microsoft Themes and other interesting log targets. You can find the link to the Provided Sinks. 
You can enrich serilog with additional information such as a session id or web request id. You can configure the output format with placeholders and configure json instead of plain text output. You can explore all the additional opportunities Serlog provides in the wiki on the github project.


### BONUS : Seq
- We use Seq technology to visualize log data. The interface we call Seq visualizes the logs we obtain.
- You need to install the Seq server. It can be installed via Docker (https://hub.docker.com/r/datalust/seq/)
- You need to run the following commands for the installation process with Docker.

**docker pull datalust**
**docker run --name Seq -e ACCEPT_EULA=Y -p 5341:80 datalust/seq:latest**

- Now Seq will be running on http://localhost:5341.
- To include Seq in the project, you need to do the following steps. You need to download Seq from Nuget Package Manager.

  ![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/8c78156c-9d0c-4140-a0b9-bff002467536)

- Add the following command in Program.cs and the logs will appear in the Seq interface.

  ![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/d91f5943-e3db-4038-8683-0a91692e9397)

**Here are the logs in Seq!**

![image](https://github.com/KardelRuveyda/serilog-demo/assets/33912144/bcab0f8d-df73-4606-9a4a-1b1f40f3d1fd)

Happy Coding!
See you next time!






  
