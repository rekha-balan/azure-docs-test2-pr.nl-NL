---
title: Common startup tasks for Cloud Services | Microsoft Docs
description: Provides some examples of common startup tasks you may want to perform in your cloud services web role or worker role.
services: cloud-services
documentationcenter: ''
author: jpconnock
manager: timlt
editor: ''
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeconnoc
ms.openlocfilehash: c9f0707f6d24ba899c89bf19066994ae860a69d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44823997"
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="78488-103">Common Cloud Service startup tasks</span><span class="sxs-lookup"><span data-stu-id="78488-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="78488-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span><span class="sxs-lookup"><span data-stu-id="78488-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="78488-105">You can use startup tasks to perform operations before a role starts.</span><span class="sxs-lookup"><span data-stu-id="78488-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="78488-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span><span class="sxs-lookup"><span data-stu-id="78488-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="78488-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="78488-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span><span class="sxs-lookup"><span data-stu-id="78488-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="78488-109">Define environment variables before a role starts</span><span class="sxs-lookup"><span data-stu-id="78488-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="78488-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span><span class="sxs-lookup"><span data-stu-id="78488-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="78488-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span><span class="sxs-lookup"><span data-stu-id="78488-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="78488-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span><span class="sxs-lookup"><span data-stu-id="78488-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="78488-113">Configure IIS startup with AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="78488-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="78488-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span><span class="sxs-lookup"><span data-stu-id="78488-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="78488-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span><span class="sxs-lookup"><span data-stu-id="78488-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="78488-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span><span class="sxs-lookup"><span data-stu-id="78488-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="78488-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span><span class="sxs-lookup"><span data-stu-id="78488-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="78488-118">Startup tasks can be run more than once between reboots.</span><span class="sxs-lookup"><span data-stu-id="78488-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="78488-119">For instance, when a role recycles.</span><span class="sxs-lookup"><span data-stu-id="78488-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="78488-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span><span class="sxs-lookup"><span data-stu-id="78488-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="78488-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span><span class="sxs-lookup"><span data-stu-id="78488-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="78488-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="78488-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="78488-123">For example, when *AppCmd.exe* generates an error.</span><span class="sxs-lookup"><span data-stu-id="78488-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="78488-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span><span class="sxs-lookup"><span data-stu-id="78488-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="78488-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span><span class="sxs-lookup"><span data-stu-id="78488-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="78488-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="78488-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="78488-127">Example of managing the error level</span><span class="sxs-lookup"><span data-stu-id="78488-127">Example of managing the error level</span></span>
<span data-ttu-id="78488-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span><span class="sxs-lookup"><span data-stu-id="78488-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="78488-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span><span class="sxs-lookup"><span data-stu-id="78488-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="78488-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span><span class="sxs-lookup"><span data-stu-id="78488-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="78488-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span><span class="sxs-lookup"><span data-stu-id="78488-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="78488-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="78488-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="78488-133">Add firewall rules</span><span class="sxs-lookup"><span data-stu-id="78488-133">Add firewall rules</span></span>
<span data-ttu-id="78488-134">In Azure, there are effectively two firewalls.</span><span class="sxs-lookup"><span data-stu-id="78488-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="78488-135">The first firewall controls connections between the virtual machine and the outside world.</span><span class="sxs-lookup"><span data-stu-id="78488-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="78488-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span><span class="sxs-lookup"><span data-stu-id="78488-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="78488-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78488-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="78488-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span><span class="sxs-lookup"><span data-stu-id="78488-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="78488-139">Azure creates firewall rules for the processes started within your roles.</span><span class="sxs-lookup"><span data-stu-id="78488-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="78488-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span><span class="sxs-lookup"><span data-stu-id="78488-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="78488-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span><span class="sxs-lookup"><span data-stu-id="78488-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="78488-142">These firewall rules can be created by using a startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="78488-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span><span class="sxs-lookup"><span data-stu-id="78488-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="78488-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span><span class="sxs-lookup"><span data-stu-id="78488-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="78488-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span><span class="sxs-lookup"><span data-stu-id="78488-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="78488-146">In this example, the startup task requires security and encryption for TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="78488-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="78488-147">Block a specific IP address</span><span class="sxs-lookup"><span data-stu-id="78488-147">Block a specific IP address</span></span>
<span data-ttu-id="78488-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span><span class="sxs-lookup"><span data-stu-id="78488-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="78488-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span><span class="sxs-lookup"><span data-stu-id="78488-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="78488-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span><span class="sxs-lookup"><span data-stu-id="78488-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="78488-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="78488-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="78488-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span><span class="sxs-lookup"><span data-stu-id="78488-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="78488-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span><span class="sxs-lookup"><span data-stu-id="78488-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

<span data-ttu-id="78488-154">Add this command to the **startup.cmd** file:</span><span class="sxs-lookup"><span data-stu-id="78488-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="78488-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span><span class="sxs-lookup"><span data-stu-id="78488-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="78488-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="78488-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="78488-157">This sample config **allows** all IPs to access the server except the two defined</span><span class="sxs-lookup"><span data-stu-id="78488-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="78488-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span><span class="sxs-lookup"><span data-stu-id="78488-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="78488-159">Create a PowerShell startup task</span><span class="sxs-lookup"><span data-stu-id="78488-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="78488-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span><span class="sxs-lookup"><span data-stu-id="78488-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="78488-161">PowerShell (by default) does not run unsigned scripts.</span><span class="sxs-lookup"><span data-stu-id="78488-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="78488-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span><span class="sxs-lookup"><span data-stu-id="78488-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="78488-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="78488-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="78488-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78488-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="78488-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span><span class="sxs-lookup"><span data-stu-id="78488-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="78488-166">Create files in local storage from a startup task</span><span class="sxs-lookup"><span data-stu-id="78488-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="78488-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span><span class="sxs-lookup"><span data-stu-id="78488-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="78488-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span><span class="sxs-lookup"><span data-stu-id="78488-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="78488-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="78488-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span><span class="sxs-lookup"><span data-stu-id="78488-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="78488-171">Then the startup task and the application are able to read and write files to the local storage resource.</span><span class="sxs-lookup"><span data-stu-id="78488-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="78488-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span><span class="sxs-lookup"><span data-stu-id="78488-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="78488-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span><span class="sxs-lookup"><span data-stu-id="78488-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="78488-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="78488-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="78488-175">Run in the emulator or cloud</span><span class="sxs-lookup"><span data-stu-id="78488-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="78488-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span><span class="sxs-lookup"><span data-stu-id="78488-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="78488-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span><span class="sxs-lookup"><span data-stu-id="78488-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="78488-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span><span class="sxs-lookup"><span data-stu-id="78488-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="78488-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span><span class="sxs-lookup"><span data-stu-id="78488-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="78488-180">You then test that environment variable for a value in your startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="78488-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="78488-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="78488-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span><span class="sxs-lookup"><span data-stu-id="78488-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="78488-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span><span class="sxs-lookup"><span data-stu-id="78488-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="78488-184">Here is a .cmd shell script that checks for that environment variable.</span><span class="sxs-lookup"><span data-stu-id="78488-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="78488-185">Detect that your task has already run</span><span class="sxs-lookup"><span data-stu-id="78488-185">Detect that your task has already run</span></span>
<span data-ttu-id="78488-186">The role may recycle without a reboot causing your startup tasks to run again.</span><span class="sxs-lookup"><span data-stu-id="78488-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="78488-187">There is no flag to indicate that a task has already run on the hosting VM.</span><span class="sxs-lookup"><span data-stu-id="78488-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="78488-188">You may have some tasks where it doesn't matter that they run multiple times.</span><span class="sxs-lookup"><span data-stu-id="78488-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="78488-189">However, you may run into a situation where you need to prevent a task from running more than once.</span><span class="sxs-lookup"><span data-stu-id="78488-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="78488-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span><span class="sxs-lookup"><span data-stu-id="78488-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="78488-191">Here is a sample cmd shell script that does that for you.</span><span class="sxs-lookup"><span data-stu-id="78488-191">Here is a sample cmd shell script that does that for you.</span></span>

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%PathToApp1Install%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%PathToApp1Install%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="78488-192">Task best practices</span><span class="sxs-lookup"><span data-stu-id="78488-192">Task best practices</span></span>
<span data-ttu-id="78488-193">Here are some best practices you should follow when configuring task for your web or worker role.</span><span class="sxs-lookup"><span data-stu-id="78488-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="78488-194">Always log startup activities</span><span class="sxs-lookup"><span data-stu-id="78488-194">Always log startup activities</span></span>
<span data-ttu-id="78488-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span><span class="sxs-lookup"><span data-stu-id="78488-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="78488-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span><span class="sxs-lookup"><span data-stu-id="78488-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="78488-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span><span class="sxs-lookup"><span data-stu-id="78488-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="78488-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span><span class="sxs-lookup"><span data-stu-id="78488-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="78488-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span><span class="sxs-lookup"><span data-stu-id="78488-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="78488-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="78488-201">You can enforce task logging by creating a wrapper that handles logging for you.</span><span class="sxs-lookup"><span data-stu-id="78488-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="78488-202">This wrapper calls the real batch file you want to run.</span><span class="sxs-lookup"><span data-stu-id="78488-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="78488-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span><span class="sxs-lookup"><span data-stu-id="78488-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="78488-204">The following example shows how to redirect all output from a startup batch file.</span><span class="sxs-lookup"><span data-stu-id="78488-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="78488-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="78488-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="78488-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="78488-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="78488-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="78488-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="78488-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="78488-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="78488-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="78488-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="78488-210">Sample output in the **StartupLog.txt** file:</span><span class="sxs-lookup"><span data-stu-id="78488-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="78488-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span><span class="sxs-lookup"><span data-stu-id="78488-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="78488-212">Set executionContext appropriately for startup tasks</span><span class="sxs-lookup"><span data-stu-id="78488-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="78488-213">Set privileges appropriately for the startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="78488-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span><span class="sxs-lookup"><span data-stu-id="78488-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="78488-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span><span class="sxs-lookup"><span data-stu-id="78488-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="78488-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span><span class="sxs-lookup"><span data-stu-id="78488-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="78488-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span><span class="sxs-lookup"><span data-stu-id="78488-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="78488-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span><span class="sxs-lookup"><span data-stu-id="78488-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="78488-219">**AppCmd.exe** requires `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="78488-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="78488-220">Use the appropriate taskType</span><span class="sxs-lookup"><span data-stu-id="78488-220">Use the appropriate taskType</span></span>
<span data-ttu-id="78488-221">The [taskType][Task] attribute determines the way the startup task is executed.</span><span class="sxs-lookup"><span data-stu-id="78488-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="78488-222">There are three values: **simple**, **background**, and **foreground**.</span><span class="sxs-lookup"><span data-stu-id="78488-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="78488-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span><span class="sxs-lookup"><span data-stu-id="78488-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="78488-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span><span class="sxs-lookup"><span data-stu-id="78488-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="78488-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span><span class="sxs-lookup"><span data-stu-id="78488-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="78488-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span><span class="sxs-lookup"><span data-stu-id="78488-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="78488-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span><span class="sxs-lookup"><span data-stu-id="78488-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="78488-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span><span class="sxs-lookup"><span data-stu-id="78488-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="78488-229">End batch files with EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="78488-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="78488-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span><span class="sxs-lookup"><span data-stu-id="78488-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="78488-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span><span class="sxs-lookup"><span data-stu-id="78488-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="78488-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span><span class="sxs-lookup"><span data-stu-id="78488-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="78488-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span><span class="sxs-lookup"><span data-stu-id="78488-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="78488-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="78488-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="78488-235">You can omit the `/B` parameter in this case.</span><span class="sxs-lookup"><span data-stu-id="78488-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="78488-236">Expect startup tasks to run more than once</span><span class="sxs-lookup"><span data-stu-id="78488-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="78488-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span><span class="sxs-lookup"><span data-stu-id="78488-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="78488-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span><span class="sxs-lookup"><span data-stu-id="78488-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="78488-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="78488-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="78488-240">Use local storage to store files that must be accessed in the role</span><span class="sxs-lookup"><span data-stu-id="78488-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="78488-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span><span class="sxs-lookup"><span data-stu-id="78488-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="78488-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="78488-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78488-243">Next steps</span><span class="sxs-lookup"><span data-stu-id="78488-243">Next steps</span></span>
<span data-ttu-id="78488-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="78488-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="78488-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span><span class="sxs-lookup"><span data-stu-id="78488-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="78488-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span><span class="sxs-lookup"><span data-stu-id="78488-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
