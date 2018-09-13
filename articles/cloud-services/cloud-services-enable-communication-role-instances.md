---
title: Communication for Roles in Cloud Services | Microsoft Docs
description: Role instances in Cloud Services can have endpoints (http, https, tcp, udp) defined for them that communicate with the outside or between other role instances.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 1b3a565387a3adc10361d003c067f6d7c0864cd5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661382"
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="33de6-103">Enable communication for role instances in azure</span><span class="sxs-lookup"><span data-stu-id="33de6-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="33de6-104">Cloud service roles communicate through internal and external connections.</span><span class="sxs-lookup"><span data-stu-id="33de6-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="33de6-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span><span class="sxs-lookup"><span data-stu-id="33de6-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="33de6-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span><span class="sxs-lookup"><span data-stu-id="33de6-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="33de6-107">Input endpoint</span><span class="sxs-lookup"><span data-stu-id="33de6-107">Input endpoint</span></span>
<span data-ttu-id="33de6-108">The input endpoint is used when you want to expose a port to the outside.</span><span class="sxs-lookup"><span data-stu-id="33de6-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="33de6-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="33de6-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="33de6-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span><span class="sxs-lookup"><span data-stu-id="33de6-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="33de6-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="33de6-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="33de6-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span><span class="sxs-lookup"><span data-stu-id="33de6-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="33de6-113">Instance input endpoint</span><span class="sxs-lookup"><span data-stu-id="33de6-113">Instance input endpoint</span></span>
<span data-ttu-id="33de6-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="33de6-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="33de6-115">You can specify a single public-facing port, or a range of ports.</span><span class="sxs-lookup"><span data-stu-id="33de6-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="33de6-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span><span class="sxs-lookup"><span data-stu-id="33de6-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="33de6-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span><span class="sxs-lookup"><span data-stu-id="33de6-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="33de6-118">Internal endpoint</span><span class="sxs-lookup"><span data-stu-id="33de6-118">Internal endpoint</span></span>
<span data-ttu-id="33de6-119">Internal endpoints are available for instance-to-instance communication.</span><span class="sxs-lookup"><span data-stu-id="33de6-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="33de6-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="33de6-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="33de6-121">A port range can be used.</span><span class="sxs-lookup"><span data-stu-id="33de6-121">A port range can be used.</span></span> <span data-ttu-id="33de6-122">There is a limit of five internal endpoints per role.</span><span class="sxs-lookup"><span data-stu-id="33de6-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="33de6-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span><span class="sxs-lookup"><span data-stu-id="33de6-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="33de6-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span><span class="sxs-lookup"><span data-stu-id="33de6-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="33de6-125">You can also use a port range.</span><span class="sxs-lookup"><span data-stu-id="33de6-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="33de6-126">Worker roles vs. Web roles</span><span class="sxs-lookup"><span data-stu-id="33de6-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="33de6-127">There is one minor difference with endpoints when working with both worker and web roles.</span><span class="sxs-lookup"><span data-stu-id="33de6-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="33de6-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span><span class="sxs-lookup"><span data-stu-id="33de6-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="33de6-129">Using the .NET SDK to access an endpoint</span><span class="sxs-lookup"><span data-stu-id="33de6-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="33de6-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span><span class="sxs-lookup"><span data-stu-id="33de6-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="33de6-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span><span class="sxs-lookup"><span data-stu-id="33de6-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="33de6-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span><span class="sxs-lookup"><span data-stu-id="33de6-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="33de6-133">You cannot obtain data about role instances running in a different service.</span><span class="sxs-lookup"><span data-stu-id="33de6-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="33de6-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span><span class="sxs-lookup"><span data-stu-id="33de6-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="33de6-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span><span class="sxs-lookup"><span data-stu-id="33de6-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="33de6-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span><span class="sxs-lookup"><span data-stu-id="33de6-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="33de6-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span><span class="sxs-lookup"><span data-stu-id="33de6-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="33de6-138">The **Instances** property returns a collection of **RoleInstance** objects.</span><span class="sxs-lookup"><span data-stu-id="33de6-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="33de6-139">This collection always contains the current instance.</span><span class="sxs-lookup"><span data-stu-id="33de6-139">This collection always contains the current instance.</span></span> <span data-ttu-id="33de6-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span><span class="sxs-lookup"><span data-stu-id="33de6-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="33de6-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span><span class="sxs-lookup"><span data-stu-id="33de6-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="33de6-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="33de6-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="33de6-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span><span class="sxs-lookup"><span data-stu-id="33de6-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="33de6-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span><span class="sxs-lookup"><span data-stu-id="33de6-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="33de6-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span><span class="sxs-lookup"><span data-stu-id="33de6-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="33de6-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span><span class="sxs-lookup"><span data-stu-id="33de6-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="33de6-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span><span class="sxs-lookup"><span data-stu-id="33de6-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="33de6-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span><span class="sxs-lookup"><span data-stu-id="33de6-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="33de6-149">Here is an example that iterates role instances.</span><span class="sxs-lookup"><span data-stu-id="33de6-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="33de6-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span><span class="sxs-lookup"><span data-stu-id="33de6-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="33de6-151">This code will only work for a deployed service.</span><span class="sxs-lookup"><span data-stu-id="33de6-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="33de6-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span><span class="sxs-lookup"><span data-stu-id="33de6-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="33de6-153">Network traffic rules to control role communication</span><span class="sxs-lookup"><span data-stu-id="33de6-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="33de6-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="33de6-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="33de6-155">The following diagram shows some common scenarios for controlling role communication:</span><span class="sxs-lookup"><span data-stu-id="33de6-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="33de6-156">![Network Traffic Rules Scenarios](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span><span class="sxs-lookup"><span data-stu-id="33de6-156">![Network Traffic Rules Scenarios](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="33de6-157">The following code example shows role definitions for the roles shown in the previous diagram.</span><span class="sxs-lookup"><span data-stu-id="33de6-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="33de6-158">Each role definition includes at least one internal endpoint defined:</span><span class="sxs-lookup"><span data-stu-id="33de6-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="33de6-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span><span class="sxs-lookup"><span data-stu-id="33de6-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="33de6-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span><span class="sxs-lookup"><span data-stu-id="33de6-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="33de6-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span><span class="sxs-lookup"><span data-stu-id="33de6-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="33de6-162">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="33de6-162">Scenario 1</span></span>
<span data-ttu-id="33de6-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="33de6-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="33de6-164">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="33de6-164">Scenario 2</span></span>
<span data-ttu-id="33de6-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="33de6-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="33de6-166">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="33de6-166">Scenario 3</span></span>
<span data-ttu-id="33de6-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="33de6-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="33de6-168">Scenario 4</span><span class="sxs-lookup"><span data-stu-id="33de6-168">Scenario 4</span></span>
<span data-ttu-id="33de6-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="33de6-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="33de6-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="33de6-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33de6-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="33de6-171">Next steps</span></span>
<span data-ttu-id="33de6-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="33de6-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>


