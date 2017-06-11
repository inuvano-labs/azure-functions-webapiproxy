# azure-functions-webapiproxy

Overview
--------
This project will create a proxy between the Azure Function request pipeline and your back-end WebAPI.
The accompanying Createfunctions.tt T4 template will start up an in-memory Owin server containing all discovered Apicontrollers in your project and create auto generated code files which automatically map to your WebAPI Routes.

Getting Started
------------------

The easiest way to get started is to set this up in an existing Visual Studio Solution containing your WebAPI project. 

Prereq.
- Azure SDK (latest)
- You'll need NPM installed (https://www.npmjs.com/package/npm)
- Once you have node/npm install "azure-functions-cli" package

1) Open your existing solution in Visual studio containing your WebAPI Project
2) Add a new "ASP.NET Web Application" project - select "Blank" when prompted
3) Configure Azure Function debugging support
3.1) Right click on the project > Properties > Web
3.2) Set "Start external Program"
3.3) For the program to start enter "C:\Users\%YOUR-USER-NAME%\node_modules\azure-functions-cli\bin\func.exe" (replacing %YOUR-USER-NAME% with your windows user name
3.4) Command Line: host start
3.5) Working directory: The full path to the visual studio project root (easiest is to right click on the project and select Open File in File Explorer)
3.6) Save
3.7) Right click "Set as Startup project"
4) Add a reference to the vs project containing your WebAPI
4.1) Rebuild the solution
5) Add a nuget reference to "Inuvano.Labs.Azure.Functions.WebApiProxy"
6) Visual Studio may/maynot run the T4 template (see Troubleshooting notes below)
7) The T4 template will create auto generated code files which map to your WebAPI routes
8) Start the Azure Storage Emulator (local storage is required)
9) F5 to run the project under debug
9.1) The Azure Function CLI will launch which allows you to run Azure Functions locally
9.2) The CLI window will detail all API routes discovered, use your favourite tool (Fiddler, Postman etc) to test the endpoints
9.3) As full debugging is supported, you can set a breakpoint in your WebAPI controller action(s).

Adding new API Routes
------------------------

1) In your WebAPI project add your Actions as you would normally
2) Rebuild the project
3) Right click on "CreateFunctions.tt" > Run Custom Tool
4) New Actions will be discovered and proxy code created automatically

Deployment
------------------------

1) Simply publish the Azure Functions project to Azure using Azure App Service publish profile

Limitations
---------------------

- Removing/renaming actions within your WebAPI does not remove/rename them from the Azure Functions project. You will need to delete the function folder manually at this time

Advanced
--------------------

- Bindings - TO FOLLOW

Troubleshooting
--------------------

- Ocassionally Visual Studio may throw an exception when running the T4 template, this can be resolved by rebuilding the project/solution and/or restarting visual studio - this will be looked into resolving in future releases
