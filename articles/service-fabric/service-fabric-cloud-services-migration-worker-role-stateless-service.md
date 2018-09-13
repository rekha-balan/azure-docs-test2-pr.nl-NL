---
title: Convert Azure Cloud Services apps to Service Fabric | Microsoft Docs
description: This guide compares Cloud Services Web and Worker Roles and Service Fabric stateless services to help migrate from Cloud Services to Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/02/2017
ms.author: vturecek
ms.openlocfilehash: 34479df8475d10fdd1d69f5d48bbe09a1727b10a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783060"
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="b4d41-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="b4d41-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="b4d41-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span><span class="sxs-lookup"><span data-stu-id="b4d41-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="b4d41-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span><span class="sxs-lookup"><span data-stu-id="b4d41-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="b4d41-106">Cloud Service project to Service Fabric application project</span><span class="sxs-lookup"><span data-stu-id="b4d41-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="b4d41-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span><span class="sxs-lookup"><span data-stu-id="b4d41-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="b4d41-108">A Cloud Service project contains one or more Web or Worker Roles.</span><span class="sxs-lookup"><span data-stu-id="b4d41-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="b4d41-109">Similarly, a Service Fabric Application project contains one or more services.</span><span class="sxs-lookup"><span data-stu-id="b4d41-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="b4d41-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="b4d41-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="b4d41-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span><span class="sxs-lookup"><span data-stu-id="b4d41-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Service Fabric and Cloud Services project comparison][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="b4d41-113">Worker Role to stateless service</span><span class="sxs-lookup"><span data-stu-id="b4d41-113">Worker Role to stateless service</span></span>
<span data-ttu-id="b4d41-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span><span class="sxs-lookup"><span data-stu-id="b4d41-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="b4d41-115">Each instance is not expected to remember the previous request.</span><span class="sxs-lookup"><span data-stu-id="b4d41-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="b4d41-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span><span class="sxs-lookup"><span data-stu-id="b4d41-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="b4d41-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span><span class="sxs-lookup"><span data-stu-id="b4d41-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="b4d41-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span><span class="sxs-lookup"><span data-stu-id="b4d41-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![Worker Role to Stateless Service][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="b4d41-120">Web Role to stateless service</span><span class="sxs-lookup"><span data-stu-id="b4d41-120">Web Role to stateless service</span></span>
<span data-ttu-id="b4d41-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span><span class="sxs-lookup"><span data-stu-id="b4d41-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="b4d41-122">However, unlike Web Roles, Service Fabric does not support IIS.</span><span class="sxs-lookup"><span data-stu-id="b4d41-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="b4d41-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="b4d41-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="b4d41-124">**Application**</span><span class="sxs-lookup"><span data-stu-id="b4d41-124">**Application**</span></span> | <span data-ttu-id="b4d41-125">**Supported**</span><span class="sxs-lookup"><span data-stu-id="b4d41-125">**Supported**</span></span> | <span data-ttu-id="b4d41-126">**Migration path**</span><span class="sxs-lookup"><span data-stu-id="b4d41-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4d41-127">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="b4d41-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="b4d41-128">No</span><span class="sxs-lookup"><span data-stu-id="b4d41-128">No</span></span> |<span data-ttu-id="b4d41-129">Convert to ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="b4d41-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="b4d41-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b4d41-130">ASP.NET MVC</span></span> |<span data-ttu-id="b4d41-131">With Migration</span><span class="sxs-lookup"><span data-stu-id="b4d41-131">With Migration</span></span> |<span data-ttu-id="b4d41-132">Upgrade to ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="b4d41-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="b4d41-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="b4d41-133">ASP.NET Web API</span></span> |<span data-ttu-id="b4d41-134">With Migration</span><span class="sxs-lookup"><span data-stu-id="b4d41-134">With Migration</span></span> |<span data-ttu-id="b4d41-135">Use self-hosted server or ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="b4d41-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="b4d41-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="b4d41-136">ASP.NET Core 1</span></span> |<span data-ttu-id="b4d41-137">Yes</span><span class="sxs-lookup"><span data-stu-id="b4d41-137">Yes</span></span> |<span data-ttu-id="b4d41-138">N/A</span><span class="sxs-lookup"><span data-stu-id="b4d41-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="b4d41-139">Entry point API and lifecycle</span><span class="sxs-lookup"><span data-stu-id="b4d41-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="b4d41-140">Worker Role and Service Fabric service APIs offer similar entry points:</span><span class="sxs-lookup"><span data-stu-id="b4d41-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="b4d41-141">**Entry Point**</span><span class="sxs-lookup"><span data-stu-id="b4d41-141">**Entry Point**</span></span> | <span data-ttu-id="b4d41-142">**Worker Role**</span><span class="sxs-lookup"><span data-stu-id="b4d41-142">**Worker Role**</span></span> | <span data-ttu-id="b4d41-143">**Service Fabric service**</span><span class="sxs-lookup"><span data-stu-id="b4d41-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4d41-144">Processing</span><span class="sxs-lookup"><span data-stu-id="b4d41-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="b4d41-145">VM start</span><span class="sxs-lookup"><span data-stu-id="b4d41-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="b4d41-146">N/A</span><span class="sxs-lookup"><span data-stu-id="b4d41-146">N/A</span></span> |
| <span data-ttu-id="b4d41-147">VM stop</span><span class="sxs-lookup"><span data-stu-id="b4d41-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="b4d41-148">N/A</span><span class="sxs-lookup"><span data-stu-id="b4d41-148">N/A</span></span> |
| <span data-ttu-id="b4d41-149">Open listener for client requests</span><span class="sxs-lookup"><span data-stu-id="b4d41-149">Open listener for client requests</span></span> |<span data-ttu-id="b4d41-150">N/A</span><span class="sxs-lookup"><span data-stu-id="b4d41-150">N/A</span></span> |<ul><li> <span data-ttu-id="b4d41-151">`CreateServiceInstanceListener()` for stateless</span><span class="sxs-lookup"><span data-stu-id="b4d41-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="b4d41-152">`CreateServiceReplicaListener()` for stateful</span><span class="sxs-lookup"><span data-stu-id="b4d41-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="b4d41-153">Worker Role</span><span class="sxs-lookup"><span data-stu-id="b4d41-153">Worker Role</span></span>
```csharp

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="b4d41-154">Service Fabric Stateless Service</span><span class="sxs-lookup"><span data-stu-id="b4d41-154">Service Fabric Stateless Service</span></span>
```csharp

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="b4d41-155">Both have a primary "Run" override in which to begin processing.</span><span class="sxs-lookup"><span data-stu-id="b4d41-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="b4d41-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="b4d41-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="b4d41-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span><span class="sxs-lookup"><span data-stu-id="b4d41-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="b4d41-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span><span class="sxs-lookup"><span data-stu-id="b4d41-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="b4d41-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span><span class="sxs-lookup"><span data-stu-id="b4d41-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="b4d41-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span><span class="sxs-lookup"><span data-stu-id="b4d41-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="b4d41-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span><span class="sxs-lookup"><span data-stu-id="b4d41-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="b4d41-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span><span class="sxs-lookup"><span data-stu-id="b4d41-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="b4d41-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span><span class="sxs-lookup"><span data-stu-id="b4d41-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="b4d41-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span><span class="sxs-lookup"><span data-stu-id="b4d41-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="b4d41-165">Application API and environment</span><span class="sxs-lookup"><span data-stu-id="b4d41-165">Application API and environment</span></span>
<span data-ttu-id="b4d41-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span><span class="sxs-lookup"><span data-stu-id="b4d41-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="b4d41-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span><span class="sxs-lookup"><span data-stu-id="b4d41-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="b4d41-168">**Environment Task**</span><span class="sxs-lookup"><span data-stu-id="b4d41-168">**Environment Task**</span></span> | <span data-ttu-id="b4d41-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="b4d41-169">**Cloud Services**</span></span> | <span data-ttu-id="b4d41-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b4d41-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4d41-171">Configuration Settings and change notification</span><span class="sxs-lookup"><span data-stu-id="b4d41-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="b4d41-172">Local Storage</span><span class="sxs-lookup"><span data-stu-id="b4d41-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="b4d41-173">Endpoint Information</span><span class="sxs-lookup"><span data-stu-id="b4d41-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="b4d41-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="b4d41-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="b4d41-175">Other roles and instance: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="b4d41-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="b4d41-176">`NodeContext` for current Node address</span><span class="sxs-lookup"><span data-stu-id="b4d41-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="b4d41-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span><span class="sxs-lookup"><span data-stu-id="b4d41-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="b4d41-178">Environment Emulation</span><span class="sxs-lookup"><span data-stu-id="b4d41-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="b4d41-179">N/A</span><span class="sxs-lookup"><span data-stu-id="b4d41-179">N/A</span></span> |
| <span data-ttu-id="b4d41-180">Simultaneous change event</span><span class="sxs-lookup"><span data-stu-id="b4d41-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="b4d41-181">N/A</span><span class="sxs-lookup"><span data-stu-id="b4d41-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="b4d41-182">Configuration settings</span><span class="sxs-lookup"><span data-stu-id="b4d41-182">Configuration settings</span></span>
<span data-ttu-id="b4d41-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span><span class="sxs-lookup"><span data-stu-id="b4d41-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="b4d41-184">These settings are key-value pairs set in ServiceConfiguration.\*.cscfg files and can be accessed directly through RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="b4d41-184">These settings are key-value pairs set in ServiceConfiguration.\*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="b4d41-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span><span class="sxs-lookup"><span data-stu-id="b4d41-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="b4d41-186">A service is composed of three packages:</span><span class="sxs-lookup"><span data-stu-id="b4d41-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="b4d41-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span><span class="sxs-lookup"><span data-stu-id="b4d41-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="b4d41-188">**Config:** all configuration files and settings for a service.</span><span class="sxs-lookup"><span data-stu-id="b4d41-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="b4d41-189">**Data:** static data files associated with the service.</span><span class="sxs-lookup"><span data-stu-id="b4d41-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="b4d41-190">Each of these packages can be independently versioned and upgraded.</span><span class="sxs-lookup"><span data-stu-id="b4d41-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="b4d41-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span><span class="sxs-lookup"><span data-stu-id="b4d41-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="b4d41-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span><span class="sxs-lookup"><span data-stu-id="b4d41-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="b4d41-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span><span class="sxs-lookup"><span data-stu-id="b4d41-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="b4d41-194">Accessing configuration</span><span class="sxs-lookup"><span data-stu-id="b4d41-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="b4d41-195">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b4d41-195">Cloud Services</span></span>
<span data-ttu-id="b4d41-196">Configuration settings from ServiceConfiguration.\*.cscfg can be accessed through `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="b4d41-196">Configuration settings from ServiceConfiguration.\*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="b4d41-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span><span class="sxs-lookup"><span data-stu-id="b4d41-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```csharp

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="b4d41-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4d41-198">Service Fabric</span></span>
<span data-ttu-id="b4d41-199">Each service has its own individual configuration package.</span><span class="sxs-lookup"><span data-stu-id="b4d41-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="b4d41-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span><span class="sxs-lookup"><span data-stu-id="b4d41-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="b4d41-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span><span class="sxs-lookup"><span data-stu-id="b4d41-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="b4d41-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="b4d41-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

```csharp

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="b4d41-203">Configuration update events</span><span class="sxs-lookup"><span data-stu-id="b4d41-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="b4d41-204">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b4d41-204">Cloud Services</span></span>
<span data-ttu-id="b4d41-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span><span class="sxs-lookup"><span data-stu-id="b4d41-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="b4d41-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span><span class="sxs-lookup"><span data-stu-id="b4d41-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```csharp

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="b4d41-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4d41-207">Service Fabric</span></span>
<span data-ttu-id="b4d41-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span><span class="sxs-lookup"><span data-stu-id="b4d41-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="b4d41-209">A service can contain multiple packages of each type.</span><span class="sxs-lookup"><span data-stu-id="b4d41-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="b4d41-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span><span class="sxs-lookup"><span data-stu-id="b4d41-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="b4d41-211">These events are available to consume changes in service packages without restarting the service instance.</span><span class="sxs-lookup"><span data-stu-id="b4d41-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```csharp

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="b4d41-212">Startup tasks</span><span class="sxs-lookup"><span data-stu-id="b4d41-212">Startup tasks</span></span>
<span data-ttu-id="b4d41-213">Startup tasks are actions that are taken before an application starts.</span><span class="sxs-lookup"><span data-stu-id="b4d41-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="b4d41-214">A startup task is typically used to run setup scripts using elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="b4d41-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="b4d41-215">Both Cloud Services and Service Fabric support start-up tasks.</span><span class="sxs-lookup"><span data-stu-id="b4d41-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="b4d41-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span><span class="sxs-lookup"><span data-stu-id="b4d41-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="b4d41-217">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4d41-217">Service Fabric</span></span> | <span data-ttu-id="b4d41-218">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b4d41-218">Cloud Services</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4d41-219">Configuration location</span><span class="sxs-lookup"><span data-stu-id="b4d41-219">Configuration location</span></span> |<span data-ttu-id="b4d41-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="b4d41-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="b4d41-221">Privileges</span><span class="sxs-lookup"><span data-stu-id="b4d41-221">Privileges</span></span> |<span data-ttu-id="b4d41-222">"limited" or "elevated"</span><span class="sxs-lookup"><span data-stu-id="b4d41-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="b4d41-223">Sequencing</span><span class="sxs-lookup"><span data-stu-id="b4d41-223">Sequencing</span></span> |<span data-ttu-id="b4d41-224">"simple", "background", "foreground"</span><span class="sxs-lookup"><span data-stu-id="b4d41-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="b4d41-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b4d41-225">Cloud Services</span></span>
<span data-ttu-id="b4d41-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="b4d41-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="b4d41-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4d41-227">Service Fabric</span></span>
<span data-ttu-id="b4d41-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="b4d41-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="b4d41-229">A note about development environment</span><span class="sxs-lookup"><span data-stu-id="b4d41-229">A note about development environment</span></span>
<span data-ttu-id="b4d41-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d41-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="b4d41-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span><span class="sxs-lookup"><span data-stu-id="b4d41-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="b4d41-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="b4d41-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="b4d41-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span><span class="sxs-lookup"><span data-stu-id="b4d41-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4d41-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4d41-234">Next steps</span></span>
<span data-ttu-id="b4d41-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span><span class="sxs-lookup"><span data-stu-id="b4d41-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="b4d41-236">Getting started with Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b4d41-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="b4d41-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4d41-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
