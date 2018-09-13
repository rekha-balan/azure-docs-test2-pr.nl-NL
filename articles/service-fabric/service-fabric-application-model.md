---
title: Azure Service Fabric application model | Microsoft Docs
description: How to model and describe applications and services in Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 3/02/2017
ms.author: ryanwi
ms.openlocfilehash: 2223338038d14f3895db3069ce2c9db29e5d808c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550416"
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="43c26-103">Model an application in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="43c26-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="43c26-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span><span class="sxs-lookup"><span data-stu-id="43c26-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="43c26-105">Understand the application model</span><span class="sxs-lookup"><span data-stu-id="43c26-105">Understand the application model</span></span>
<span data-ttu-id="43c26-106">An application is a collection of constituent services that perform a certain function or functions.</span><span class="sxs-lookup"><span data-stu-id="43c26-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="43c26-107">A service performs a complete and standalone function (it can start and run independently of other services) and is composed of code, configuration, and data.</span><span class="sxs-lookup"><span data-stu-id="43c26-107">A service performs a complete and standalone function (it can start and run independently of other services) and is composed of code, configuration, and data.</span></span> <span data-ttu-id="43c26-108">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span><span class="sxs-lookup"><span data-stu-id="43c26-108">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="43c26-109">Each component in this hierarchical application model can be versioned and upgraded independently.</span><span class="sxs-lookup"><span data-stu-id="43c26-109">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![The Service Fabric application model][appmodel-diagram]

<span data-ttu-id="43c26-111">An application type is a categorization of an application and consists of a bundle of service types.</span><span class="sxs-lookup"><span data-stu-id="43c26-111">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="43c26-112">A service type is a categorization of a service.</span><span class="sxs-lookup"><span data-stu-id="43c26-112">A service type is a categorization of a service.</span></span> <span data-ttu-id="43c26-113">The categorization can have different settings and configurations, but the core functionality remains the same.</span><span class="sxs-lookup"><span data-stu-id="43c26-113">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="43c26-114">The instances of a service are the different service configuration variations of the same service type.</span><span class="sxs-lookup"><span data-stu-id="43c26-114">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="43c26-115">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests) that are the templates against which applications can be instantiated from the cluster's image store.</span><span class="sxs-lookup"><span data-stu-id="43c26-115">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests) that are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="43c26-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="43c26-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="43c26-117">The code for different application instances will run as separate processes even when hosted by the same Service Fabric node.</span><span class="sxs-lookup"><span data-stu-id="43c26-117">The code for different application instances will run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="43c26-118">Furthermore, the lifecycle of each application instance can be managed (i.e. upgraded) independently.</span><span class="sxs-lookup"><span data-stu-id="43c26-118">Furthermore, the lifecycle of each application instance can be managed (i.e. upgraded) independently.</span></span> <span data-ttu-id="43c26-119">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and packages.</span><span class="sxs-lookup"><span data-stu-id="43c26-119">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and packages.</span></span> <span data-ttu-id="43c26-120">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all of those package types.</span><span class="sxs-lookup"><span data-stu-id="43c26-120">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all of those package types.</span></span>

![Service Fabric application types and service types][cluster-imagestore-apptypes]

<span data-ttu-id="43c26-122">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span><span class="sxs-lookup"><span data-stu-id="43c26-122">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="43c26-123">These are covered in detail in the ensuing sections.</span><span class="sxs-lookup"><span data-stu-id="43c26-123">These are covered in detail in the ensuing sections.</span></span>

<span data-ttu-id="43c26-124">There can be one or more instances of a service type active in the cluster.</span><span class="sxs-lookup"><span data-stu-id="43c26-124">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="43c26-125">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="43c26-125">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="43c26-126">This replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span><span class="sxs-lookup"><span data-stu-id="43c26-126">This replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="43c26-127">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="43c26-127">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="43c26-128">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span><span class="sxs-lookup"><span data-stu-id="43c26-128">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Partitions and replicas within a service][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="43c26-130">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="43c26-130">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="43c26-131">For more details, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="43c26-131">For more details, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="43c26-132">Describe a service</span><span class="sxs-lookup"><span data-stu-id="43c26-132">Describe a service</span></span>
<span data-ttu-id="43c26-133">The service manifest declaratively defines the service type and version.</span><span class="sxs-lookup"><span data-stu-id="43c26-133">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="43c26-134">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span><span class="sxs-lookup"><span data-stu-id="43c26-134">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="43c26-135">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span><span class="sxs-lookup"><span data-stu-id="43c26-135">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="43c26-136">Here is a simple example service manifest:</span><span class="sxs-lookup"><span data-stu-id="43c26-136">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="43c26-137">**Version** attributes are unstructured strings and not parsed by the system.</span><span class="sxs-lookup"><span data-stu-id="43c26-137">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="43c26-138">These are used to version each component for upgrades.</span><span class="sxs-lookup"><span data-stu-id="43c26-138">These are used to version each component for upgrades.</span></span>

<span data-ttu-id="43c26-139">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span><span class="sxs-lookup"><span data-stu-id="43c26-139">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="43c26-140">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span><span class="sxs-lookup"><span data-stu-id="43c26-140">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="43c26-141">The resulting processes are expected to register the supported service types at run time.</span><span class="sxs-lookup"><span data-stu-id="43c26-141">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="43c26-142">Note that service types are declared at the manifest level and not the code package level.</span><span class="sxs-lookup"><span data-stu-id="43c26-142">Note that service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="43c26-143">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span><span class="sxs-lookup"><span data-stu-id="43c26-143">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="43c26-144">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span><span class="sxs-lookup"><span data-stu-id="43c26-144">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="43c26-145">The executable specified by **EntryPoint** is typically the long-running service host.</span><span class="sxs-lookup"><span data-stu-id="43c26-145">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="43c26-146">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span><span class="sxs-lookup"><span data-stu-id="43c26-146">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="43c26-147">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span><span class="sxs-lookup"><span data-stu-id="43c26-147">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="43c26-148">The resulting process is monitored and restarted (beginning again with **SetupEntryPoint**) if it ever terminates or crashes.</span><span class="sxs-lookup"><span data-stu-id="43c26-148">The resulting process is monitored and restarted (beginning again with **SetupEntryPoint**) if it ever terminates or crashes.</span></span> 

<span data-ttu-id="43c26-149">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="43c26-149">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="43c26-150">For example:</span><span class="sxs-lookup"><span data-stu-id="43c26-150">For example:</span></span>

* <span data-ttu-id="43c26-151">Setting up and initializing environment variables that the service executable needs.</span><span class="sxs-lookup"><span data-stu-id="43c26-151">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="43c26-152">This is not limited to only executables written via the Service Fabric programming models.</span><span class="sxs-lookup"><span data-stu-id="43c26-152">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="43c26-153">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span><span class="sxs-lookup"><span data-stu-id="43c26-153">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="43c26-154">Setting up access control by installing security certificates.</span><span class="sxs-lookup"><span data-stu-id="43c26-154">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="43c26-155">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="43c26-155">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="43c26-156">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span><span class="sxs-lookup"><span data-stu-id="43c26-156">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="43c26-157">These can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span><span class="sxs-lookup"><span data-stu-id="43c26-157">These can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="43c26-158">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span><span class="sxs-lookup"><span data-stu-id="43c26-158">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="43c26-159">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span><span class="sxs-lookup"><span data-stu-id="43c26-159">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="43c26-160">This file contains sections of user-defined, key-value pair settings that the process can read back at run time.</span><span class="sxs-lookup"><span data-stu-id="43c26-160">This file contains sections of user-defined, key-value pair settings that the process can read back at run time.</span></span> <span data-ttu-id="43c26-161">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span><span class="sxs-lookup"><span data-stu-id="43c26-161">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="43c26-162">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span><span class="sxs-lookup"><span data-stu-id="43c26-162">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="43c26-163">Here is an example *Settings.xml* file:</span><span class="sxs-lookup"><span data-stu-id="43c26-163">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="43c26-164">A service manifest can contain multiple code, configuration, and data packages.</span><span class="sxs-lookup"><span data-stu-id="43c26-164">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="43c26-165">Each of those can be versioned independently.</span><span class="sxs-lookup"><span data-stu-id="43c26-165">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="43c26-166">Describe an application</span><span class="sxs-lookup"><span data-stu-id="43c26-166">Describe an application</span></span>
<span data-ttu-id="43c26-167">The application manifest declaratively describes the application type and version.</span><span class="sxs-lookup"><span data-stu-id="43c26-167">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="43c26-168">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span><span class="sxs-lookup"><span data-stu-id="43c26-168">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="43c26-169">The load-balancing domains into which the application is placed are also described.</span><span class="sxs-lookup"><span data-stu-id="43c26-169">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="43c26-170">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span><span class="sxs-lookup"><span data-stu-id="43c26-170">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="43c26-171">Here is a simple example application manifest:</span><span class="sxs-lookup"><span data-stu-id="43c26-171">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="43c26-172">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span><span class="sxs-lookup"><span data-stu-id="43c26-172">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="43c26-173">These are also used to version each component for upgrades.</span><span class="sxs-lookup"><span data-stu-id="43c26-173">These are also used to version each component for upgrades.</span></span>

<span data-ttu-id="43c26-174">**ServiceManifestImport** contains references to service manifests that compose this application type.</span><span class="sxs-lookup"><span data-stu-id="43c26-174">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="43c26-175">Imported service manifests determine what service types are valid within this application type.</span><span class="sxs-lookup"><span data-stu-id="43c26-175">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="43c26-176">Within the ServiceManifestImport you can override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span><span class="sxs-lookup"><span data-stu-id="43c26-176">Within the ServiceManifestImport you can override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="43c26-177">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span><span class="sxs-lookup"><span data-stu-id="43c26-177">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="43c26-178">Default services are just a convenience and behave like normal services in every respect after they have been created.</span><span class="sxs-lookup"><span data-stu-id="43c26-178">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="43c26-179">They are upgraded along with any other services in the application instance and can be removed as well.</span><span class="sxs-lookup"><span data-stu-id="43c26-179">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="43c26-180">An application manifest can contain multiple service manifest imports and default services.</span><span class="sxs-lookup"><span data-stu-id="43c26-180">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="43c26-181">Each service manifest import can be versioned independently.</span><span class="sxs-lookup"><span data-stu-id="43c26-181">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="43c26-182">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="43c26-182">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="43c26-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="43c26-183">Next steps</span></span>
<span data-ttu-id="43c26-184">[Package an application](service-fabric-package-apps.md) and get it ready to deploy.</span><span class="sxs-lookup"><span data-stu-id="43c26-184">[Package an application](service-fabric-package-apps.md) and get it ready to deploy.</span></span>

<span data-ttu-id="43c26-185">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span><span class="sxs-lookup"><span data-stu-id="43c26-185">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="43c26-186">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span><span class="sxs-lookup"><span data-stu-id="43c26-186">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="43c26-187">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span><span class="sxs-lookup"><span data-stu-id="43c26-187">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[appmodel-diagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md



