---
title: Run Startup Tasks in Azure Cloud Services | Microsoft Docs
description: Startup tasks help prepare your cloud service environment for your app. This teaches you how startup tasks work and how to make them
services: cloud-services
documentationcenter: ''
author: jpconnock
manager: timlt
editor: ''
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeconnoc
ms.openlocfilehash: 6601eba90f3c3644d418ddd0a74746e1a12bcbd3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826774"
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="cbd3b-104">How to configure and run startup tasks for a cloud service</span><span class="sxs-lookup"><span data-stu-id="cbd3b-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="cbd3b-105">You can use startup tasks to perform operations before a role starts.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="cbd3b-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="cbd3b-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="cbd3b-108">How startup tasks work</span><span class="sxs-lookup"><span data-stu-id="cbd3b-108">How startup tasks work</span></span>
<span data-ttu-id="cbd3b-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="cbd3b-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="cbd3b-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="cbd3b-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="cbd3b-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="cbd3b-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="cbd3b-115">Startup tasks can also be executed several times between reboots.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="cbd3b-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="cbd3b-117">Startup tasks should be written in a way that allows them to run several times without problems.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="cbd3b-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="cbd3b-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="cbd3b-120">Role startup order</span><span class="sxs-lookup"><span data-stu-id="cbd3b-120">Role startup order</span></span>
<span data-ttu-id="cbd3b-121">The following lists the role startup procedure in Azure:</span><span class="sxs-lookup"><span data-stu-id="cbd3b-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="cbd3b-122">The instance is marked as **Starting** and does not receive traffic.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="cbd3b-123">All startup tasks are executed according to their **taskType** attribute.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="cbd3b-124">The **simple** tasks are executed synchronously, one at a time.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="cbd3b-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="cbd3b-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="cbd3b-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbd3b-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="cbd3b-128">The role host process is started and the site is created in IIS.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="cbd3b-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="cbd3b-130">The instance is marked as **Ready** and traffic is routed to the instance.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="cbd3b-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="cbd3b-132">Example of a startup task</span><span class="sxs-lookup"><span data-stu-id="cbd3b-132">Example of a startup task</span></span>
<span data-ttu-id="cbd3b-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="cbd3b-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="cbd3b-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="cbd3b-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="cbd3b-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="cbd3b-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="cbd3b-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="cbd3b-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="cbd3b-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span><span class="sxs-lookup"><span data-stu-id="cbd3b-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="cbd3b-140">Description of task attributes</span><span class="sxs-lookup"><span data-stu-id="cbd3b-140">Description of task attributes</span></span>
<span data-ttu-id="cbd3b-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span><span class="sxs-lookup"><span data-stu-id="cbd3b-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="cbd3b-142">**commandLine** - Specifies the command line for the startup task:</span><span class="sxs-lookup"><span data-stu-id="cbd3b-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="cbd3b-143">The command, with optional command line parameters, which begins the startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="cbd3b-144">Frequently this is the filename of a .cmd or .bat batch file.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="cbd3b-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="cbd3b-146">Environment variables are not expanded in determining the path and file of the task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="cbd3b-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="cbd3b-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="cbd3b-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="cbd3b-149">**executionContext** - Specifies the privilege level for the startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="cbd3b-150">The privilege level can be limited or elevated:</span><span class="sxs-lookup"><span data-stu-id="cbd3b-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="cbd3b-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="cbd3b-151">**limited**</span></span>  
  <span data-ttu-id="cbd3b-152">The startup task runs with the same privileges as the role.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="cbd3b-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="cbd3b-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="cbd3b-154">**elevated**</span></span>  
  <span data-ttu-id="cbd3b-155">The startup task runs with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="cbd3b-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="cbd3b-157">The privilege level of a startup task does not need to be the same as the role itself.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="cbd3b-158">**taskType** - Specifies the way a startup task is executed.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="cbd3b-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="cbd3b-159">**simple**</span></span>  
  <span data-ttu-id="cbd3b-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="cbd3b-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="cbd3b-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="cbd3b-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="cbd3b-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="cbd3b-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="cbd3b-166">**background**</span><span class="sxs-lookup"><span data-stu-id="cbd3b-166">**background**</span></span>  
  <span data-ttu-id="cbd3b-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="cbd3b-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="cbd3b-168">**foreground**</span></span>  
  <span data-ttu-id="cbd3b-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="cbd3b-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="cbd3b-171">The **background** tasks do not have this restriction.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="cbd3b-172">Environment variables</span><span class="sxs-lookup"><span data-stu-id="cbd3b-172">Environment variables</span></span>
<span data-ttu-id="cbd3b-173">Environment variables are a way to pass information to a startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="cbd3b-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="cbd3b-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="cbd3b-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="cbd3b-177">Static environment variables uses the **value** attribute of the [Variable] element.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="cbd3b-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="cbd3b-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="cbd3b-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="cbd3b-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="cbd3b-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="cbd3b-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="cbd3b-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="cbd3b-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span><span class="sxs-lookup"><span data-stu-id="cbd3b-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="cbd3b-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="cbd3b-184">Next steps</span></span>
<span data-ttu-id="cbd3b-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="cbd3b-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="cbd3b-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
