---
title: Reliable Services WCF communication stack | Microsoft Docs
description: The built-in WCF communication stack in Service Fabric provides client-service WCF communication for Reliable Services.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/25/2017
ms.author: bharatn
ms.openlocfilehash: eb5589b14a037601a1e655f7b7a160fa1f5bbcb7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563449"
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="0d7cf-103">WCF-based communication stack for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0d7cf-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="0d7cf-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="0d7cf-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="0d7cf-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="0d7cf-107">WCF Communication Listener</span><span class="sxs-lookup"><span data-stu-id="0d7cf-107">WCF Communication Listener</span></span>
<span data-ttu-id="0d7cf-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="0d7cf-109">Lest say we have a service contract of type `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="0d7cf-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="0d7cf-110">We can create a WCF communication listener in the service the following manner.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="0d7cf-111">Writing clients for the WCF communication stack</span><span class="sxs-lookup"><span data-stu-id="0d7cf-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="0d7cf-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="0d7cf-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="0d7cf-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="0d7cf-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="0d7cf-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="0d7cf-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span><span class="sxs-lookup"><span data-stu-id="0d7cf-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0d7cf-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d7cf-117">Next steps</span></span>
* [<span data-ttu-id="0d7cf-118">Remote procedure call with Reliable Services remoting</span><span class="sxs-lookup"><span data-stu-id="0d7cf-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="0d7cf-119">Web API with OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0d7cf-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="0d7cf-120">Securing communication for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0d7cf-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

