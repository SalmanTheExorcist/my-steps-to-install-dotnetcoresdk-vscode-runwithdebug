# my-steps-to-install-dotnetcoresdk-vscode-runwithdebug

### [Documenting my steps to install dotnet-sdk-8.0.11 on my Asus Notebook running GarudaLinux-Cinammon x64, creating my first Asp.Net Core MVC Web App and Run-with-Debug in VSCode]
------------------------------------------------------------
### [Friday November 22nd, 2024 @ 21:12 PM (Bahrain-Local-Time)]

------------------------------------------------------------
### (Note): It took me many attempts to get this right, with VSCode Run-with-Debug to work.  So, decided to document the steps for future reference.

-------------------------------------------------------------
### (Note): "fish" and "bash" shells.

-------------------------------------------------------------

### References:

#### (.NET 8.0 SDK (v8.0.404) - Linux x64 Binaries) ==> **URL: https://dotnet.microsoft.com/en-us/download/dotnet/8.0**


#### (MS.Learn-Docs - DotNetCore8 Manual Install on Linux)==>**URL: https://learn.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual#manual-install**


#### ("fish shell" set - display and change shell variables)==>**URL: https://fishshell.com/docs/current/cmds/set.html**


#### (StackExchange How to check if a directory exists in Linux command line?)==>**URL: https://superuser.com/questions/98825/how-to-check-if-a-directory-exists-in-linux-command-line**


#### ("fish shell" - fish_add_path command)==>**URL: https://fishshell.com/docs/current/cmds/fish_add_path.html**


#### (Enforce HTTPS in ASP.NET Core - Linux )==>**URL: https://aka.ms/dotnet-https-linux**

#### (Enforce HTTPS in ASP.NET Core - Linux )==>**URL: https://learn.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-8.0&tabs=visual-studio%2Clinux-sles#trust-https-certificate-on-linux-with-linux-dev-certs**


#### (open-source, community-supported, .NET global tool that provides a convenient way to create and trust a developer certificate on Linux. The tool is not maintained or supported by Microsoft.)==>**URL: https://github.com/tmds/linux-dev-certs**


-------------------------------------------------------------

(1)==> Downloaded the .NET 8.0 SDK (v8.0.404) - Linux x64 Binaries!

	(1-1)--> Downloaded file: "dotnet-sdk-8.0.404-linux-x64.tar.gz"

(2)==>In "fish" shell: - **[(pwd) is  $HOME Directory]**
	==>(Note): watch-out for **['single-quotes']** and **["double-quotes"]** - they give different results.

	(2-1)--> set DOTNET_FILE 'dotnet-sdk-8.0.404-linux-x64.tar.gz'
		(2-1-1)--> Verify the checksum values for the downloaded file:
--------------------------------------------------------------------------------------------------------------------

			"2f166f7f3bd508154d72d1783ffac6e0e3c92023ccc2c6de49d22b411fc8b9e6dd03e7576acc1bb5870a6951181129ba77f3bf94bb45fe9c70105b1b896b9bb9"

	(Terminal)==> sha512sum dotnet-sdk-8.0.404-linux-x64.tar.gz
	"2f166f7f3bd508154d72d1783ffac6e0e3c92023ccc2c6de49d22b411fc8b9e6dd03e7576acc1bb5870a6951181129ba77f3bf94bb45fe9c70105b1b896b9bb9"  dotnet-sdk-8.0.404-linux-x64.tar.gz

-----------------------------------------------------------------------------------------------------------------------
	(2-2)-->(To Confirm The Value): echo $DOTNET_FILE

	(2-3)-->(To Confirm The Value): echo $(pwd)/.dotnet

	(2-4)--> set -U -x DOTNET_ROOT $(pwd)/.dotnet

	(2-5)-->(To Confirm The Value): echo $DOTNET_ROOT

	(2-6)--> mkdir -p "$DOTNET_ROOT"

	(2-7)-->(Sanity Check): test -d "$DOTNET_ROOT" && echo "Directory Exists"

	(2-8)--> tar zxf "$DOTNET_FILE" -C "$DOTNET_ROOT"

	(2-9)-->(Confirm Extracted Content): ls -l "$DOTNET_ROOT"

	(2-10)--> mkdir "$DOTNET_ROOT/tools"

	(2-11)--> test -d "$DOTNET_ROOT/tools" && echo "Directory Exists"

	(2-12)--> fish_add_path -U $DOTNET_ROOT

	(2-13)--> fish_add_path -U "$DOTNET_ROOT/tools"

	(2-14)--> (To cofirm all is well thus far, I rebooted before giving VSCode a try): systemctl reboot

-----------------------------------------------------------------------------------------------------------------------------------

(3)==> After Reboot - back to "fish shell":

	(3-1)--> dotnet --version

	(3-2)--> dotnet --list-runtimes

	(3-3)--> dotnet --list-sdks

	(3-4)--> (deprecated) dotnet new --list

	(3-5)--> dotnet new list 

	(3-6)--> dotnet new list --help
------------------------------------------------------------------------------------------
	
Note: **https://github.com/tmds/linux-dev-certs** ==>The .NET dotnet dev-certs tool doesn't support trusting the ASP.NET Core HTTPS development certificate on Linux.
	This repo contains a .NET global tool that creates and installs a developer certificate on Linux.
	
	(3-7)--> dotnet tool update -g linux-dev-certs
	
			-->You can invoke the tool using the following command: dotnet-linux-dev-certs - Tool 'linux-dev-certs' (version '0.3.0') was successfully installed.

	(3-8)--> dotnet linux-dev-certs install 

			-->Creating CA certificate.
				Installing CA certificate.
				Removing existing development certificates.
				Creating development certificate.
				Installing development certificate.
				The development certificate was successfully installed.
				ASP.NET Core applications may still print a warning at startup that the developer certificate is not trusted.
				This is a false warning. The message is no longer printed with ASP.NET Core 9 preview 6+.
------------------------------------------------------------------------------------------

(4)==>Creating my first AspNetCore MVC WebApp and opening it in VSCode, Run with Debug:

	(4-1)--> mkdir MyFirstMvcWebSolution

	(4-2)--> cd MyFirstMvcWebSolution/

	(4-3)--> dotnet new mvc --name MyFirstMvcWebApp.Admin

	(4-4)--> code .

	(4-5)--> (Explorer Panel/Pane Left-Side) Exapnding the MyFirstMvcWebApp.Admin 
			--> Open the "Program.cs" file

				-->Now VSCode prompts for: Do you want to install the recommended 'C# Dev Kit' extension from Microsoft for the C# language?

				--> Clicked "Install" and watching to see what happens.

				-->Activating the Extension by signing in with my microsoft account.
				
	(4-6)-->Clicking on the "Debug" icon on the left-side activity bar/pane/panel (what ever it is called) 
		--> Selected the "C# Debugger option + (Default) Configuration"

		--> Debug-Console: "You may only use the Microsoft Visual Studio .NET/C/C++ Debugger (vsdbg) with Visual Studio Code, Visual Studio or Visual Studio for Mac software to help you develop and test your applications.

		--> My default web browser opens up with the default [controller]/[action] route.

		Good Stuff so far I suppose. 
------------------------------------------------------------------------------

	(4-7)--> (From Terminal): 
			--> cd MyFirstMvcWebApp.Admin/
			--> dotnet build
			--> dotnet run --launch-profile https
			--> Trying out the https://localhost:7149 in my browser workes too!

	

			

		
	

	

			











