---
title: Get started with Python and Azure Cloud Services | Microsoft Docs
description: Overview of using Python Tools for Visual Studio to create Azure cloud services including web roles and worker roles.
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: ''
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 11/16/2016
ms.author: adegeo
ms.openlocfilehash: 3fd4111b502d3600c5a1aeab6118533b3813229c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553528"
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="66868-103">Python web and worker roles with Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66868-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="66868-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="66868-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="66868-105">You will learn how to use Visual Studio to create and deploy a basic Cloud Service that uses Python.</span><span class="sxs-lookup"><span data-stu-id="66868-105">You will learn how to use Visual Studio to create and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66868-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="66868-106">Prerequisites</span></span>
* [<span data-ttu-id="66868-107">Visual Studio 2013, 2015, or 2017</span><span class="sxs-lookup"><span data-stu-id="66868-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="66868-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="66868-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="66868-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span><span class="sxs-lookup"><span data-stu-id="66868-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="66868-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span><span class="sxs-lookup"><span data-stu-id="66868-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="66868-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="66868-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="66868-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="66868-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="66868-113">What are Python web and worker roles?</span><span class="sxs-lookup"><span data-stu-id="66868-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="66868-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="66868-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="66868-115">All three models support Python.</span><span class="sxs-lookup"><span data-stu-id="66868-115">All three models support Python.</span></span> <span data-ttu-id="66868-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="66868-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="66868-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications, while a worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span><span class="sxs-lookup"><span data-stu-id="66868-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications, while a worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="66868-118">For more information, see [What is a Cloud Service?].</span><span class="sxs-lookup"><span data-stu-id="66868-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="66868-119">*Looking to build a simple website?*</span><span class="sxs-lookup"><span data-stu-id="66868-119">*Looking to build a simple website?*</span></span>
> <span data-ttu-id="66868-120">If your scenario involves just a simple website front-end, consider using the lightweight Web Apps feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="66868-120">If your scenario involves just a simple website front-end, consider using the lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="66868-121">You can easily upgrade to a Cloud Service as your website grows and your requirements change.</span><span class="sxs-lookup"><span data-stu-id="66868-121">You can easily upgrade to a Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="66868-122">See the <a href="/develop/python/">Python Developer Center</a> for articles that cover development of the Web Apps feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="66868-122">See the <a href="/develop/python/">Python Developer Center</a> for articles that cover development of the Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="66868-123">Project creation</span><span class="sxs-lookup"><span data-stu-id="66868-123">Project creation</span></span>
<span data-ttu-id="66868-124">In Visual Studio, you can select **Azure Cloud Service** in the **New Project** dialog box, under **Python**.</span><span class="sxs-lookup"><span data-stu-id="66868-124">In Visual Studio, you can select **Azure Cloud Service** in the **New Project** dialog box, under **Python**.</span></span>

![New Project Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="66868-126">In the Azure Cloud Service wizard, you can create new web and worker roles.</span><span class="sxs-lookup"><span data-stu-id="66868-126">In the Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Azure Cloud Service Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="66868-128">The worker role template comes with boilerplate code to connect to a Azure storage account or Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="66868-128">The worker role template comes with boilerplate code to connect to a Azure storage account or Azure Service Bus.</span></span>

![Cloud Service Solution](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="66868-130">You can add web or worker roles to an existing cloud service at any time.</span><span class="sxs-lookup"><span data-stu-id="66868-130">You can add web or worker roles to an existing cloud service at any time.</span></span>  <span data-ttu-id="66868-131">You can choose to add existing projects in your solution, or create new ones.</span><span class="sxs-lookup"><span data-stu-id="66868-131">You can choose to add existing projects in your solution, or create new ones.</span></span>

![Add Role Command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="66868-133">Your cloud service can contain roles implemented in different languages.</span><span class="sxs-lookup"><span data-stu-id="66868-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="66868-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span><span class="sxs-lookup"><span data-stu-id="66868-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="66868-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span><span class="sxs-lookup"><span data-stu-id="66868-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-the-cloud-service"></a><span data-ttu-id="66868-136">Install Python on the cloud service</span><span class="sxs-lookup"><span data-stu-id="66868-136">Install Python on the cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="66868-137">The setup scripts that are installed with Visual Studio (at the time this article was last updated) do not work.</span><span class="sxs-lookup"><span data-stu-id="66868-137">The setup scripts that are installed with Visual Studio (at the time this article was last updated) do not work.</span></span> <span data-ttu-id="66868-138">This section describes a workaround.</span><span class="sxs-lookup"><span data-stu-id="66868-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="66868-139">The main problem with the setup scripts are that they do not install python.</span><span class="sxs-lookup"><span data-stu-id="66868-139">The main problem with the setup scripts are that they do not install python.</span></span> <span data-ttu-id="66868-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in the [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span><span class="sxs-lookup"><span data-stu-id="66868-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in the [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="66868-141">The first task (**PrepPython.ps1**) downloads and installs the Python runtime.</span><span class="sxs-lookup"><span data-stu-id="66868-141">The first task (**PrepPython.ps1**) downloads and installs the Python runtime.</span></span> <span data-ttu-id="66868-142">The second task (**PipInstaller.ps1**) runs pip to install any dependencies you may have.</span><span class="sxs-lookup"><span data-stu-id="66868-142">The second task (**PipInstaller.ps1**) runs pip to install any dependencies you may have.</span></span>

<span data-ttu-id="66868-143">The scripts below were written targeting Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="66868-143">The scripts below were written targeting Python 3.5.</span></span> <span data-ttu-id="66868-144">If you want to use the version 2.x of python, set the **PYTHON2** variable file to **on** for the two startup tasks and the runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="66868-144">If you want to use the version 2.x of python, set the **PYTHON2** variable file to **on** for the two startup tasks and the runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

<span data-ttu-id="66868-145">The **PYTHON2** and **PYPATH** variables needs to be added to the worker startup task.</span><span class="sxs-lookup"><span data-stu-id="66868-145">The **PYTHON2** and **PYPATH** variables needs to be added to the worker startup task.</span></span> <span data-ttu-id="66868-146">The **PYPATH** variable is only used if the **PYTHON2** variable is set to **on**.</span><span class="sxs-lookup"><span data-stu-id="66868-146">The **PYPATH** variable is only used if the **PYTHON2** variable is set to **on**.</span></span>

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="66868-147">Sample ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="66868-147">Sample ServiceDefinition.csdef</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



<span data-ttu-id="66868-148">Next, create the **PrepPython.ps1** and **PipInstaller.ps1** files in the **./bin** folder of your role.</span><span class="sxs-lookup"><span data-stu-id="66868-148">Next, create the **PrepPython.ps1** and **PipInstaller.ps1** files in the **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="66868-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="66868-149">PrepPython.ps1</span></span>
<span data-ttu-id="66868-150">This script installs python.</span><span class="sxs-lookup"><span data-stu-id="66868-150">This script installs python.</span></span> <span data-ttu-id="66868-151">If the **PYTHON2** environment variable is set to **on** then Python 2.7 will be installed, otherwise Python 3.5 will be installed.</span><span class="sxs-lookup"><span data-stu-id="66868-151">If the **PYTHON2** environment variable is set to **on** then Python 2.7 will be installed, otherwise Python 3.5 will be installed.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url to $outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a><span data-ttu-id="66868-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="66868-152">PipInstaller.ps1</span></span>
<span data-ttu-id="66868-153">This script calls up pip and installs all of the dependencies in the **requirements.txt** file.</span><span class="sxs-lookup"><span data-stu-id="66868-153">This script calls up pip and installs all of the dependencies in the **requirements.txt** file.</span></span> <span data-ttu-id="66868-154">If the **PYTHON2** environment variable is set to **on** then Python 2.7 will be used, otherwise Python 3.5 will be used.</span><span class="sxs-lookup"><span data-stu-id="66868-154">If the **PYTHON2** environment variable is set to **on** then Python 2.7 will be used, otherwise Python 3.5 will be used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="66868-155">Modify LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="66868-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="66868-156">In the case of a **worker role** project, **LauncherWorker.ps1** file is required to execute the startup file.</span><span class="sxs-lookup"><span data-stu-id="66868-156">In the case of a **worker role** project, **LauncherWorker.ps1** file is required to execute the startup file.</span></span> <span data-ttu-id="66868-157">In a **web role** project, the startup file is instead defined in the project properties.</span><span class="sxs-lookup"><span data-stu-id="66868-157">In a **web role** project, the startup file is instead defined in the project properties.</span></span>
> 
> 

<span data-ttu-id="66868-158">The **bin\LaunchWorker.ps1** was originally created to do a lot of prep work but it doesn't really work.</span><span class="sxs-lookup"><span data-stu-id="66868-158">The **bin\LaunchWorker.ps1** was originally created to do a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="66868-159">Replace the contents in that file with the following script.</span><span class="sxs-lookup"><span data-stu-id="66868-159">Replace the contents in that file with the following script.</span></span>

<span data-ttu-id="66868-160">This script calls the **worker.py** file from your python project.</span><span class="sxs-lookup"><span data-stu-id="66868-160">This script calls the **worker.py** file from your python project.</span></span> <span data-ttu-id="66868-161">If the **PYTHON2** environment variable is set to **on** then Python 2.7 will be used, otherwise Python 3.5 will be used.</span><span class="sxs-lookup"><span data-stu-id="66868-161">If the **PYTHON2** environment variable is set to **on** then Python 2.7 will be used, otherwise Python 3.5 will be used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize to your local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a><span data-ttu-id="66868-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="66868-162">ps.cmd</span></span>
<span data-ttu-id="66868-163">The Visual Studio templates should have created a **ps.cmd** file in the **./bin** folder.</span><span class="sxs-lookup"><span data-stu-id="66868-163">The Visual Studio templates should have created a **ps.cmd** file in the **./bin** folder.</span></span> <span data-ttu-id="66868-164">This shell script calls out the PowerShell wrapper scripts above and provides logging based on the name of the PowerShell wrapper called.</span><span class="sxs-lookup"><span data-stu-id="66868-164">This shell script calls out the PowerShell wrapper scripts above and provides logging based on the name of the PowerShell wrapper called.</span></span> <span data-ttu-id="66868-165">If this file wasn't created, here is what should be in it.</span><span class="sxs-lookup"><span data-stu-id="66868-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="66868-166">Run locally</span><span class="sxs-lookup"><span data-stu-id="66868-166">Run locally</span></span>
<span data-ttu-id="66868-167">If you set your cloud service project as the startup project and press F5, the cloud service will run in the local Azure emulator.</span><span class="sxs-lookup"><span data-stu-id="66868-167">If you set your cloud service project as the startup project and press F5, the cloud service will run in the local Azure emulator.</span></span>

<span data-ttu-id="66868-168">Although PTVS supports launching in the emulator, debugging (for example, breakpoints) will not work.</span><span class="sxs-lookup"><span data-stu-id="66868-168">Although PTVS supports launching in the emulator, debugging (for example, breakpoints) will not work.</span></span>

<span data-ttu-id="66868-169">To debug your web and worker roles, you can set the role project as the startup project and debug that instead.</span><span class="sxs-lookup"><span data-stu-id="66868-169">To debug your web and worker roles, you can set the role project as the startup project and debug that instead.</span></span>  <span data-ttu-id="66868-170">You can also set multiple startup projects.</span><span class="sxs-lookup"><span data-stu-id="66868-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="66868-171">Right-click the solution and then select **Set StartUp Projects**.</span><span class="sxs-lookup"><span data-stu-id="66868-171">Right-click the solution and then select **Set StartUp Projects**.</span></span>

![Solution Startup Project Properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/startup.png)

## <a name="publish-to-azure"></a><span data-ttu-id="66868-173">Publish to Azure</span><span class="sxs-lookup"><span data-stu-id="66868-173">Publish to Azure</span></span>
<span data-ttu-id="66868-174">To publish, right-click the cloud service project in the solution and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="66868-174">To publish, right-click the cloud service project in the solution and then select **Publish**.</span></span>

![Microsoft Azure Publish Sign In](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="66868-176">Follow the wizard.</span><span class="sxs-lookup"><span data-stu-id="66868-176">Follow the wizard.</span></span> <span data-ttu-id="66868-177">If you need to, enable remote desktop.</span><span class="sxs-lookup"><span data-stu-id="66868-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="66868-178">Remote desktop is helpful when you need to debug something.</span><span class="sxs-lookup"><span data-stu-id="66868-178">Remote desktop is helpful when you need to debug something.</span></span>

<span data-ttu-id="66868-179">When you are done configuring settings, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="66868-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="66868-180">Some progress will appear in the output window, then you'll see the Microsoft Azure Activity Log window.</span><span class="sxs-lookup"><span data-stu-id="66868-180">Some progress will appear in the output window, then you'll see the Microsoft Azure Activity Log window.</span></span>

![Microsoft Azure Activity Log Window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="66868-182">Deployment will take several minutes to complete, then your web and/or worker roles will be running on Azure!</span><span class="sxs-lookup"><span data-stu-id="66868-182">Deployment will take several minutes to complete, then your web and/or worker roles will be running on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="66868-183">Investigate logs</span><span class="sxs-lookup"><span data-stu-id="66868-183">Investigate logs</span></span>
<span data-ttu-id="66868-184">After the cloud service virtual machine starts up and installs Python, you can look at the logs to find any failure messages.</span><span class="sxs-lookup"><span data-stu-id="66868-184">After the cloud service virtual machine starts up and installs Python, you can look at the logs to find any failure messages.</span></span> <span data-ttu-id="66868-185">These logs are located in the **C:\Resources\Directory\\{role}\LogFiles** folder.</span><span class="sxs-lookup"><span data-stu-id="66868-185">These logs are located in the **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="66868-186">**PrepPython.err.txt** will have at least one error in it from when the script tries to detect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span><span class="sxs-lookup"><span data-stu-id="66868-186">**PrepPython.err.txt** will have at least one error in it from when the script tries to detect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66868-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="66868-187">Next steps</span></span>
<span data-ttu-id="66868-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see the PTVS documentation:</span><span class="sxs-lookup"><span data-stu-id="66868-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see the PTVS documentation:</span></span>

* <span data-ttu-id="66868-189">[Cloud Service Projects][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="66868-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="66868-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see the following articles.</span><span class="sxs-lookup"><span data-stu-id="66868-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see the following articles.</span></span>

* <span data-ttu-id="66868-191">[Blob Service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="66868-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="66868-192">[Table Service][Table Service]</span><span class="sxs-lookup"><span data-stu-id="66868-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="66868-193">[Queue Service][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="66868-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="66868-194">[Service Bus Queues][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="66868-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="66868-195">[Service Bus Topics][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="66868-195">[Service Bus Topics][Service Bus Topics]</span></span>

<!--Link references-->

[What is a Cloud Service?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/about.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]: ../storage/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/storage-python-how-to-use-queue-storage.md
[Table Service]: ../storage/storage-python-how-to-use-table-storage.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/







