---
title: Get started with Azure Relay WCF relays in .NET | Microsoft Docs
description: Learn how to use Azure Relay WCF relays to connect two applications hosted in different locations.
services: service-bus-relay
documentationcenter: .net
author: spelluru
manager: timlt
editor: ''
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/20/2017
ms.author: spelluru
ms.openlocfilehash: b9701eae026522238424a21ae3ecf2baa40334fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828139"
---
# <a name="how-to-use-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="c224f-103">How to use Azure Relay WCF relays with .NET</span><span class="sxs-lookup"><span data-stu-id="c224f-103">How to use Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="c224f-104">This article describes how to use the Azure Relay service.</span><span class="sxs-lookup"><span data-stu-id="c224f-104">This article describes how to use the Azure Relay service.</span></span> <span data-ttu-id="c224f-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span><span class="sxs-lookup"><span data-stu-id="c224f-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span></span> <span data-ttu-id="c224f-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="c224f-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="c224f-107">What is WCF Relay?</span><span class="sxs-lookup"><span data-stu-id="c224f-107">What is WCF Relay?</span></span>

<span data-ttu-id="c224f-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span><span class="sxs-lookup"><span data-stu-id="c224f-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="c224f-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c224f-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span></span>

![WCF Relay Concepts](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="c224f-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span><span class="sxs-lookup"><span data-stu-id="c224f-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="c224f-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span><span class="sxs-lookup"><span data-stu-id="c224f-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span></span> <span data-ttu-id="c224f-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span><span class="sxs-lookup"><span data-stu-id="c224f-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span></span> <span data-ttu-id="c224f-114">Relay enables you to securely control who can access these services at a fine-grained level.</span><span class="sxs-lookup"><span data-stu-id="c224f-114">Relay enables you to securely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="c224f-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span><span class="sxs-lookup"><span data-stu-id="c224f-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span></span>

<span data-ttu-id="c224f-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span><span class="sxs-lookup"><span data-stu-id="c224f-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="c224f-117">Get the Service Bus NuGet package</span><span class="sxs-lookup"><span data-stu-id="c224f-117">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="c224f-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span><span class="sxs-lookup"><span data-stu-id="c224f-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span> <span data-ttu-id="c224f-119">To install the NuGet package in your project, do the following:</span><span class="sxs-lookup"><span data-stu-id="c224f-119">To install the NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="c224f-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c224f-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c224f-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span><span class="sxs-lookup"><span data-stu-id="c224f-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="c224f-122">Click **Install** to complete the installation, then close the following dialog box:</span><span class="sxs-lookup"><span data-stu-id="c224f-122">Click **Install** to complete the installation, then close the following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="c224f-123">Expose and consume a SOAP web service with TCP</span><span class="sxs-lookup"><span data-stu-id="c224f-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="c224f-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span><span class="sxs-lookup"><span data-stu-id="c224f-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span></span> <span data-ttu-id="c224f-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span><span class="sxs-lookup"><span data-stu-id="c224f-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="c224f-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span><span class="sxs-lookup"><span data-stu-id="c224f-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span></span>

<span data-ttu-id="c224f-127">In this task, you build a simple WCF service and add a relay listener to it.</span><span class="sxs-lookup"><span data-stu-id="c224f-127">In this task, you build a simple WCF service and add a relay listener to it.</span></span> <span data-ttu-id="c224f-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span><span class="sxs-lookup"><span data-stu-id="c224f-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span></span> <span data-ttu-id="c224f-129">Instead, it focuses on the code.</span><span class="sxs-lookup"><span data-stu-id="c224f-129">Instead, it focuses on the code.</span></span>

<span data-ttu-id="c224f-130">Before starting these steps, complete the following procedure to set up your environment:</span><span class="sxs-lookup"><span data-stu-id="c224f-130">Before starting these steps, complete the following procedure to set up your environment:</span></span>

1. <span data-ttu-id="c224f-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span><span class="sxs-lookup"><span data-stu-id="c224f-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span></span>
2. <span data-ttu-id="c224f-132">Add the Service Bus NuGet package to both projects.</span><span class="sxs-lookup"><span data-stu-id="c224f-132">Add the Service Bus NuGet package to both projects.</span></span> <span data-ttu-id="c224f-133">This package adds all the necessary assembly references to your projects.</span><span class="sxs-lookup"><span data-stu-id="c224f-133">This package adds all the necessary assembly references to your projects.</span></span>

### <a name="how-to-create-the-service"></a><span data-ttu-id="c224f-134">How to create the service</span><span class="sxs-lookup"><span data-stu-id="c224f-134">How to create the service</span></span>
<span data-ttu-id="c224f-135">First, create the service itself.</span><span class="sxs-lookup"><span data-stu-id="c224f-135">First, create the service itself.</span></span> <span data-ttu-id="c224f-136">Any WCF service consists of at least three distinct parts:</span><span class="sxs-lookup"><span data-stu-id="c224f-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="c224f-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span><span class="sxs-lookup"><span data-stu-id="c224f-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span></span>
* <span data-ttu-id="c224f-138">Implementation of that contract.</span><span class="sxs-lookup"><span data-stu-id="c224f-138">Implementation of that contract.</span></span>
* <span data-ttu-id="c224f-139">Host that hosts the WCF service and exposes several endpoints.</span><span class="sxs-lookup"><span data-stu-id="c224f-139">Host that hosts the WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="c224f-140">The code examples in this section address each of these components.</span><span class="sxs-lookup"><span data-stu-id="c224f-140">The code examples in this section address each of these components.</span></span>

<span data-ttu-id="c224f-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span><span class="sxs-lookup"><span data-stu-id="c224f-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span></span> <span data-ttu-id="c224f-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span><span class="sxs-lookup"><span data-stu-id="c224f-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span></span> <span data-ttu-id="c224f-143">Creating such an interface is considered a best practice.</span><span class="sxs-lookup"><span data-stu-id="c224f-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="c224f-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span><span class="sxs-lookup"><span data-stu-id="c224f-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="c224f-145">With the contract in place, the implementation is as follows:</span><span class="sxs-lookup"><span data-stu-id="c224f-145">With the contract in place, the implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="c224f-146">Configure a service host programmatically</span><span class="sxs-lookup"><span data-stu-id="c224f-146">Configure a service host programmatically</span></span>
<span data-ttu-id="c224f-147">With the contract and implementation in place, you can now host the service.</span><span class="sxs-lookup"><span data-stu-id="c224f-147">With the contract and implementation in place, you can now host the service.</span></span> <span data-ttu-id="c224f-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span><span class="sxs-lookup"><span data-stu-id="c224f-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span></span> <span data-ttu-id="c224f-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span><span class="sxs-lookup"><span data-stu-id="c224f-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="c224f-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span><span class="sxs-lookup"><span data-stu-id="c224f-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER to close");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="c224f-151">In the example, you create two endpoints that are on the same contract implementation.</span><span class="sxs-lookup"><span data-stu-id="c224f-151">In the example, you create two endpoints that are on the same contract implementation.</span></span> <span data-ttu-id="c224f-152">One is local and one is projected through Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="c224f-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="c224f-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span><span class="sxs-lookup"><span data-stu-id="c224f-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span></span> <span data-ttu-id="c224f-154">The local endpoint has a local network address with a distinct port.</span><span class="sxs-lookup"><span data-stu-id="c224f-154">The local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="c224f-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span><span class="sxs-lookup"><span data-stu-id="c224f-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span></span> <span data-ttu-id="c224f-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span><span class="sxs-lookup"><span data-stu-id="c224f-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="c224f-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span><span class="sxs-lookup"><span data-stu-id="c224f-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span></span> <span data-ttu-id="c224f-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span><span class="sxs-lookup"><span data-stu-id="c224f-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-the-appconfig-file"></a><span data-ttu-id="c224f-159">Configure a service host in the App.config file</span><span class="sxs-lookup"><span data-stu-id="c224f-159">Configure a service host in the App.config file</span></span>
<span data-ttu-id="c224f-160">You can also configure the host using the App.config file.</span><span class="sxs-lookup"><span data-stu-id="c224f-160">You can also configure the host using the App.config file.</span></span> <span data-ttu-id="c224f-161">The service hosting code in this case appears in the next example.</span><span class="sxs-lookup"><span data-stu-id="c224f-161">The service hosting code in this case appears in the next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER to close");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="c224f-162">The endpoint definitions move into the App.config file.</span><span class="sxs-lookup"><span data-stu-id="c224f-162">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="c224f-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="c224f-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="c224f-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span><span class="sxs-lookup"><span data-stu-id="c224f-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span></span> <span data-ttu-id="c224f-165">This code example assumes that your project C# namespace is named **Service**.</span><span class="sxs-lookup"><span data-stu-id="c224f-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="c224f-166">Replace the placeholders with your relay namespace name and SAS key.</span><span class="sxs-lookup"><span data-stu-id="c224f-166">Replace the placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="c224f-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c224f-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span></span>

### <a name="create-the-client"></a><span data-ttu-id="c224f-168">Create the client</span><span class="sxs-lookup"><span data-stu-id="c224f-168">Create the client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="c224f-169">Configure a client programmatically</span><span class="sxs-lookup"><span data-stu-id="c224f-169">Configure a client programmatically</span></span>
<span data-ttu-id="c224f-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="c224f-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="c224f-171">Service Bus uses a token-based security model implemented using SAS.</span><span class="sxs-lookup"><span data-stu-id="c224f-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="c224f-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span><span class="sxs-lookup"><span data-stu-id="c224f-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="c224f-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span><span class="sxs-lookup"><span data-stu-id="c224f-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span></span> <span data-ttu-id="c224f-174">The name and key are those obtained from the portal as described in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c224f-174">The name and key are those obtained from the portal as described in the previous section.</span></span>

<span data-ttu-id="c224f-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span><span class="sxs-lookup"><span data-stu-id="c224f-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span></span>

<span data-ttu-id="c224f-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span><span class="sxs-lookup"><span data-stu-id="c224f-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="c224f-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span><span class="sxs-lookup"><span data-stu-id="c224f-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span></span> <span data-ttu-id="c224f-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span><span class="sxs-lookup"><span data-stu-id="c224f-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span></span> <span data-ttu-id="c224f-179">The client code can also run in the cloud or locally.</span><span class="sxs-lookup"><span data-stu-id="c224f-179">The client code can also run in the cloud or locally.</span></span>

#### <a name="configure-a-client-in-the-appconfig-file"></a><span data-ttu-id="c224f-180">Configure a client in the App.config file</span><span class="sxs-lookup"><span data-stu-id="c224f-180">Configure a client in the App.config file</span></span>
<span data-ttu-id="c224f-181">The following code shows how to configure the client using the App.config file.</span><span class="sxs-lookup"><span data-stu-id="c224f-181">The following code shows how to configure the client using the App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="c224f-182">The endpoint definitions move into the App.config file.</span><span class="sxs-lookup"><span data-stu-id="c224f-182">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="c224f-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span><span class="sxs-lookup"><span data-stu-id="c224f-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span></span> <span data-ttu-id="c224f-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span><span class="sxs-lookup"><span data-stu-id="c224f-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="c224f-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="c224f-185">Next steps</span></span>
<span data-ttu-id="c224f-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="c224f-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span></span>

* [<span data-ttu-id="c224f-187">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="c224f-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="c224f-188">Azure Service Bus architectural overview</span><span class="sxs-lookup"><span data-stu-id="c224f-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="c224f-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="c224f-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
