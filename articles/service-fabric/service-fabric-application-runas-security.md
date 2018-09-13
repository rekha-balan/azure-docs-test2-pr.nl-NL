---
title: Learn about Azure microservices security policies | Microsoft Docs
description: An overview of how to run a Service Fabric application under system and local security accounts, including the SetupEntry point where an application needs to perform some privileged action before it starts
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: mfussell
ms.openlocfilehash: c2e7d1f5ab588ace76b3d2bebbc4337f148284be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563112"
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="5f811-103">Configure security policies for your application</span><span class="sxs-lookup"><span data-stu-id="5f811-103">Configure security policies for your application</span></span>
<span data-ttu-id="5f811-104">By using Azure Service Fabric, you can help secure applications that are running in the cluster under different user accounts.</span><span class="sxs-lookup"><span data-stu-id="5f811-104">By using Azure Service Fabric, you can help secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="5f811-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span><span class="sxs-lookup"><span data-stu-id="5f811-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="5f811-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span><span class="sxs-lookup"><span data-stu-id="5f811-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="5f811-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span><span class="sxs-lookup"><span data-stu-id="5f811-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="5f811-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span><span class="sxs-lookup"><span data-stu-id="5f811-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="5f811-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="5f811-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="5f811-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts.</span><span class="sxs-lookup"><span data-stu-id="5f811-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts.</span></span>

<span data-ttu-id="5f811-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span><span class="sxs-lookup"><span data-stu-id="5f811-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="5f811-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span><span class="sxs-lookup"><span data-stu-id="5f811-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="5f811-113">Configure the policy for a service setup entry point</span><span class="sxs-lookup"><span data-stu-id="5f811-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="5f811-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span><span class="sxs-lookup"><span data-stu-id="5f811-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="5f811-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span><span class="sxs-lookup"><span data-stu-id="5f811-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="5f811-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="5f811-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="5f811-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span><span class="sxs-lookup"><span data-stu-id="5f811-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="5f811-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span><span class="sxs-lookup"><span data-stu-id="5f811-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="5f811-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span><span class="sxs-lookup"><span data-stu-id="5f811-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="5f811-120">Configure the policy by using a local account</span><span class="sxs-lookup"><span data-stu-id="5f811-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="5f811-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="5f811-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="5f811-122">The following example shows how to configure the service to run under user administrator account privileges.</span><span class="sxs-lookup"><span data-stu-id="5f811-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="5f811-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="5f811-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="5f811-124">This indicates that the user is a member of the Administrators system group.</span><span class="sxs-lookup"><span data-stu-id="5f811-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="5f811-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="5f811-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="5f811-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="5f811-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="5f811-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span><span class="sxs-lookup"><span data-stu-id="5f811-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="5f811-128">This is the default account that all service entry points are run as.</span><span class="sxs-lookup"><span data-stu-id="5f811-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="5f811-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="5f811-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="5f811-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="5f811-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="5f811-131">Next, ensure that the MySetup.bat file is included in the service package.</span><span class="sxs-lookup"><span data-stu-id="5f811-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="5f811-132">By default, it is not.</span><span class="sxs-lookup"><span data-stu-id="5f811-132">By default, it is not.</span></span> <span data-ttu-id="5f811-133">Select the file, right-click to get the context menu, and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5f811-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="5f811-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span><span class="sxs-lookup"><span data-stu-id="5f811-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="5f811-135">See the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="5f811-135">See the following screenshot.</span></span>

![Visual Studio CopyToOutput for SetupEntryPoint batch file][image1]

<span data-ttu-id="5f811-137">Now open the MySetup.bat file and add the following commands:</span><span class="sxs-lookup"><span data-stu-id="5f811-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="5f811-138">Next, build and deploy the solution to a local development cluster.</span><span class="sxs-lookup"><span data-stu-id="5f811-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="5f811-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span><span class="sxs-lookup"><span data-stu-id="5f811-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="5f811-140">Open a PowerShell command prompt and type:</span><span class="sxs-lookup"><span data-stu-id="5f811-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="5f811-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span><span class="sxs-lookup"><span data-stu-id="5f811-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="5f811-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="5f811-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="5f811-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="5f811-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="5f811-144">Configure the policy by using local system accounts</span><span class="sxs-lookup"><span data-stu-id="5f811-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="5f811-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span><span class="sxs-lookup"><span data-stu-id="5f811-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="5f811-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span><span class="sxs-lookup"><span data-stu-id="5f811-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="5f811-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span><span class="sxs-lookup"><span data-stu-id="5f811-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="5f811-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="5f811-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="5f811-149">Start PowerShell commands from a setup entry point</span><span class="sxs-lookup"><span data-stu-id="5f811-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="5f811-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span><span class="sxs-lookup"><span data-stu-id="5f811-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="5f811-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="5f811-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="5f811-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span><span class="sxs-lookup"><span data-stu-id="5f811-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="5f811-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="5f811-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="5f811-154">MySetup.bat to start a PowerShell file:</span><span class="sxs-lookup"><span data-stu-id="5f811-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="5f811-155">In the PowerShell file, add the following to set a system environment variable:</span><span class="sxs-lookup"><span data-stu-id="5f811-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="5f811-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span><span class="sxs-lookup"><span data-stu-id="5f811-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="5f811-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span><span class="sxs-lookup"><span data-stu-id="5f811-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="5f811-158">To change this folder, set the working folder:</span><span class="sxs-lookup"><span data-stu-id="5f811-158">To change this folder, set the working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="5f811-159">Use console redirection for local debugging</span><span class="sxs-lookup"><span data-stu-id="5f811-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="5f811-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="5f811-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="5f811-161">To do this, you can set a console redirection policy, which writes the output to a file.</span><span class="sxs-lookup"><span data-stu-id="5f811-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="5f811-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span><span class="sxs-lookup"><span data-stu-id="5f811-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="5f811-163">(See where to find this in the preceding example.)</span><span class="sxs-lookup"><span data-stu-id="5f811-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="5f811-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span><span class="sxs-lookup"><span data-stu-id="5f811-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="5f811-165">*Only* use this for local development and debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="5f811-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="5f811-166">The following example shows setting the console redirection with a FileRetentionCount value:</span><span class="sxs-lookup"><span data-stu-id="5f811-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="5f811-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span><span class="sxs-lookup"><span data-stu-id="5f811-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="5f811-168">**After you debug your script, immediately remove this console redirection policy**.</span><span class="sxs-lookup"><span data-stu-id="5f811-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="5f811-169">Configure a policy for service code packages</span><span class="sxs-lookup"><span data-stu-id="5f811-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="5f811-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="5f811-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="5f811-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span><span class="sxs-lookup"><span data-stu-id="5f811-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="5f811-172">Create local user groups</span><span class="sxs-lookup"><span data-stu-id="5f811-172">Create local user groups</span></span>
<span data-ttu-id="5f811-173">You can define and create user groups that allow one or more users to be added to a group.</span><span class="sxs-lookup"><span data-stu-id="5f811-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="5f811-174">This is particularly useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span><span class="sxs-lookup"><span data-stu-id="5f811-174">This is particularly useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="5f811-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="5f811-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="5f811-176">Two users, Customer1 and Customer2, are made members of this local group.</span><span class="sxs-lookup"><span data-stu-id="5f811-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="5f811-177">Create local users</span><span class="sxs-lookup"><span data-stu-id="5f811-177">Create local users</span></span>
<span data-ttu-id="5f811-178">You can create a local user that can be used to help secure a service within the application.</span><span class="sxs-lookup"><span data-stu-id="5f811-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="5f811-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="5f811-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="5f811-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span><span class="sxs-lookup"><span data-stu-id="5f811-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="5f811-181">Instead, they are dynamically generated and have random passwords.</span><span class="sxs-lookup"><span data-stu-id="5f811-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="5f811-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span><span class="sxs-lookup"><span data-stu-id="5f811-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="5f811-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that will be used to generate the same password across all machines.</span><span class="sxs-lookup"><span data-stu-id="5f811-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that will be used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="5f811-184">Assign policies to the service code packages</span><span class="sxs-lookup"><span data-stu-id="5f811-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="5f811-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span><span class="sxs-lookup"><span data-stu-id="5f811-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="5f811-186">It also associates code packages from the service manifest with user accounts in the principals section.</span><span class="sxs-lookup"><span data-stu-id="5f811-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="5f811-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span><span class="sxs-lookup"><span data-stu-id="5f811-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="5f811-188">The following example shows different policies being applied:</span><span class="sxs-lookup"><span data-stu-id="5f811-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="5f811-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span><span class="sxs-lookup"><span data-stu-id="5f811-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="5f811-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span><span class="sxs-lookup"><span data-stu-id="5f811-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="5f811-191">The actual service code can run under a lower-privilege account.</span><span class="sxs-lookup"><span data-stu-id="5f811-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="5f811-192">Apply a default policy to all service code packages</span><span class="sxs-lookup"><span data-stu-id="5f811-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="5f811-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span><span class="sxs-lookup"><span data-stu-id="5f811-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="5f811-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span><span class="sxs-lookup"><span data-stu-id="5f811-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="5f811-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span><span class="sxs-lookup"><span data-stu-id="5f811-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="5f811-196">Use an Active Directory domain group or user</span><span class="sxs-lookup"><span data-stu-id="5f811-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="5f811-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span><span class="sxs-lookup"><span data-stu-id="5f811-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="5f811-198">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f811-198">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5f811-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span><span class="sxs-lookup"><span data-stu-id="5f811-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="5f811-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="5f811-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="5f811-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span><span class="sxs-lookup"><span data-stu-id="5f811-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="5f811-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span><span class="sxs-lookup"><span data-stu-id="5f811-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="5f811-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5f811-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="5f811-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span><span class="sxs-lookup"><span data-stu-id="5f811-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```


## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="5f811-205">Assign a security access policy for HTTP and HTTPS endpoints</span><span class="sxs-lookup"><span data-stu-id="5f811-205">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="5f811-206">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span><span class="sxs-lookup"><span data-stu-id="5f811-206">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="5f811-207">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span><span class="sxs-lookup"><span data-stu-id="5f811-207">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="5f811-208">The following example applies the Customer3 account to an endpoint called **ServiceEndpointName**, which gives it full access rights.</span><span class="sxs-lookup"><span data-stu-id="5f811-208">The following example applies the Customer3 account to an endpoint called **ServiceEndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="5f811-209">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span><span class="sxs-lookup"><span data-stu-id="5f811-209">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="5f811-210">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="5f811-210">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```


## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="5f811-211">A complete application manifest example</span><span class="sxs-lookup"><span data-stu-id="5f811-211">A complete application manifest example</span></span>
<span data-ttu-id="5f811-212">The following application manifest shows many of the different settings:</span><span class="sxs-lookup"><span data-stu-id="5f811-212">The following application manifest shows many of the different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="5f811-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f811-213">Next steps</span></span>
* [<span data-ttu-id="5f811-214">Understand the application model</span><span class="sxs-lookup"><span data-stu-id="5f811-214">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="5f811-215">Specify resources in a service manifest</span><span class="sxs-lookup"><span data-stu-id="5f811-215">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="5f811-216">Deploy an application</span><span class="sxs-lookup"><span data-stu-id="5f811-216">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-runas-security/copy-to-output.png

