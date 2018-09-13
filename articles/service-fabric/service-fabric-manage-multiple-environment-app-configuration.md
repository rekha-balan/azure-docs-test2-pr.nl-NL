---
title: Manage multiple environments in Service Fabric | Microsoft Docs
description: Service Fabric applications can be run on clusters that range in size from one machine to thousands of machines. In some cases, you will want to configure your application differently for those varied environments. This article covers how to define different application parameters per environment.
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/06/2017
ms.author: seanmck
ms.openlocfilehash: 9ddb435994ffe0d6a2a5e1f6b12d29d2fe99f570
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554762"
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="7ecd8-105">Manage application parameters for multiple environments</span><span class="sxs-lookup"><span data-stu-id="7ecd8-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="7ecd8-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="7ecd8-107">While application binaries can run without modification across this wide spectrum of environments, you will often want to configure the application differently, depending on the number of machines you're deploying to.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-107">While application binaries can run without modification across this wide spectrum of environments, you will often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="7ecd8-108">As a simple example, consider `InstanceCount` for a stateless service.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="7ecd8-109">When you are running applications in Azure, you will generally want to set this parameter to the special value of "-1".</span><span class="sxs-lookup"><span data-stu-id="7ecd8-109">When you are running applications in Azure, you will generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="7ecd8-110">This ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span><span class="sxs-lookup"><span data-stu-id="7ecd8-110">This ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="7ecd8-111">However, this configuration is not suitable for a single-machine cluster since you can't have multiple processes listening on the same endpoint on a single machine.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-111">However, this configuration is not suitable for a single-machine cluster since you can't have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="7ecd8-112">Instead, you will typically set `InstanceCount` to "1".</span><span class="sxs-lookup"><span data-stu-id="7ecd8-112">Instead, you will typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="7ecd8-113">Specifying environment-specific parameters</span><span class="sxs-lookup"><span data-stu-id="7ecd8-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="7ecd8-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="7ecd8-115">Default services and application parameters are configured in the application and service manifests.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="7ecd8-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="7ecd8-117">Default services</span><span class="sxs-lookup"><span data-stu-id="7ecd8-117">Default services</span></span>
<span data-ttu-id="7ecd8-118">Service Fabric applications are made up of a collection of service instances.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="7ecd8-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="7ecd8-120">These are referred to as "default services".</span><span class="sxs-lookup"><span data-stu-id="7ecd8-120">These are referred to as "default services".</span></span> <span data-ttu-id="7ecd8-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span><span class="sxs-lookup"><span data-stu-id="7ecd8-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
    <DefaultServices>
        <Service Name="Stateful1">
            <StatefulService
                ServiceTypeName="Stateful1Type"
                TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
                MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

                <UniformInt64Partition
                    PartitionCount="[Stateful1_PartitionCount]"
                    LowKey="-9223372036854775808"
                    HighKey="9223372036854775807"
                />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="7ecd8-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span><span class="sxs-lookup"><span data-stu-id="7ecd8-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="2" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="7ecd8-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="7ecd8-124">Not all service instance parameters are suitable for per-environment configuration.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="7ecd8-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="7ecd8-126">Per-environment service configuration settings</span><span class="sxs-lookup"><span data-stu-id="7ecd8-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="7ecd8-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="7ecd8-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="7ecd8-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span><span class="sxs-lookup"><span data-stu-id="7ecd8-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
    <Section Name="MyConfigSection">
      <Parameter Name="MaxQueueSize" Value="25" />
    </Section>
```
<span data-ttu-id="7ecd8-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

```xml
    <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="7ecd8-131">This parameter can then be configured by environment as shown above.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="7ecd8-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="7ecd8-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="7ecd8-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="7ecd8-135">Setting and using environment variables</span><span class="sxs-lookup"><span data-stu-id="7ecd8-135">Setting and using environment variables</span></span> 
<span data-ttu-id="7ecd8-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="7ecd8-137">The example below shows two environment variables, one with a value set and the other will be overridden.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-137">The example below shows two environment variables, one with a value set and the other will be overridden.</span></span> <span data-ttu-id="7ecd8-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
<span data-ttu-id="7ecd8-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="7ecd8-140">Once the named service instance is created you can access the environment variables from code.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="7ecd8-141">e.g. In C# you can do the following</span><span class="sxs-lookup"><span data-stu-id="7ecd8-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="7ecd8-142">Service Fabric environment variables</span><span class="sxs-lookup"><span data-stu-id="7ecd8-142">Service Fabric environment variables</span></span>
<span data-ttu-id="7ecd8-143">Service Fabric has built in environment variables set for each service instance.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="7ecd8-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="7ecd8-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="7ecd8-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="7ecd8-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="7ecd8-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="7ecd8-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="7ecd8-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="7ecd8-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="7ecd8-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="7ecd8-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="7ecd8-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="7ecd8-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="7ecd8-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="7ecd8-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="7ecd8-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="7ecd8-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="7ecd8-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="7ecd8-156">Fabric_NodeId</span></span>
* <span data-ttu-id="7ecd8-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="7ecd8-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="7ecd8-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="7ecd8-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="7ecd8-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="7ecd8-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="7ecd8-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="7ecd8-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="7ecd8-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="7ecd8-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="7ecd8-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="7ecd8-163">FabricPackageFileName</span></span>

<span data-ttu-id="7ecd8-164">The code belows shows how to list the Service Fabric environment variables</span><span class="sxs-lookup"><span data-stu-id="7ecd8-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="7ecd8-165">Below are example environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-165">Below are example environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="7ecd8-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="7ecd8-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="7ecd8-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="7ecd8-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="7ecd8-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="7ecd8-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="7ecd8-171">Application parameter files</span><span class="sxs-lookup"><span data-stu-id="7ecd8-171">Application parameter files</span></span>
<span data-ttu-id="7ecd8-172">The Service Fabric application project can include one or more application parameter files.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="7ecd8-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span><span class="sxs-lookup"><span data-stu-id="7ecd8-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="2" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="7ecd8-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="7ecd8-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Application parameter files in Solution Explorer][app-parameters-solution-explorer]

<span data-ttu-id="7ecd8-176">To create a new parameter file, simply copy and paste an existing one and give it a new name.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-176">To create a new parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="7ecd8-177">Identifying environment-specific parameters during deployment</span><span class="sxs-lookup"><span data-stu-id="7ecd8-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="7ecd8-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="7ecd8-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="7ecd8-180">Deploy from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ecd8-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="7ecd8-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Choose a parameter file in the Publish dialog][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="7ecd8-183">Deploy from PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ecd8-183">Deploy from PowerShell</span></span>
<span data-ttu-id="7ecd8-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span><span class="sxs-lookup"><span data-stu-id="7ecd8-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="7ecd8-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ecd8-185">Next steps</span></span>
<span data-ttu-id="7ecd8-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ecd8-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="7ecd8-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="7ecd8-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png


