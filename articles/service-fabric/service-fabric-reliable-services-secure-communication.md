---
title: Secure service remoting communications with C# in Azure Service Fabric | Microsoft Docs
description: Learn how to secure service remoting based communication for C# reliable services that are running in an Azure Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 1148bc1f8c0ff5b0a83d5a98b2e4539b9dbbdba2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824270"
---
# <a name="secure-service-remoting-communications-in-a-c-service"></a><span data-ttu-id="7f25a-103">Secure service remoting communications in a C# service</span><span class="sxs-lookup"><span data-stu-id="7f25a-103">Secure service remoting communications in a C# service</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java on Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="7f25a-106">Security is one of the most important aspects of communication.</span><span class="sxs-lookup"><span data-stu-id="7f25a-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="7f25a-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span><span class="sxs-lookup"><span data-stu-id="7f25a-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="7f25a-108">This article discusses how to improve security when you're using service remoting in a C# service.</span><span class="sxs-lookup"><span data-stu-id="7f25a-108">This article discusses how to improve security when you're using service remoting in a C# service.</span></span> <span data-ttu-id="7f25a-109">It builds on an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services written in C#.</span><span class="sxs-lookup"><span data-stu-id="7f25a-109">It builds on an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services written in C#.</span></span> 

<span data-ttu-id="7f25a-110">To help secure a service when you're using service remoting with C# services, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7f25a-110">To help secure a service when you're using service remoting with C# services, follow these steps:</span></span>

1. <span data-ttu-id="7f25a-111">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span><span class="sxs-lookup"><span data-stu-id="7f25a-111">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="7f25a-112">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span><span class="sxs-lookup"><span data-stu-id="7f25a-112">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="7f25a-113">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span><span class="sxs-lookup"><span data-stu-id="7f25a-113">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="7f25a-114">Add listener settings and security credentials.</span><span class="sxs-lookup"><span data-stu-id="7f25a-114">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="7f25a-115">Make sure the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="7f25a-115">Make sure the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> 
    
    > [!NOTE]
    > On Linux nodes, the certificate must be present as PEM-formatted files in the */var/lib/sfcerts* directory. To learn more, see [Location and format of X.509 certificates on Linux nodes](./service-fabric-configure-certificates-linux.md#location-and-format-of-x509-certificates-on-linux-nodes). 

    <span data-ttu-id="7f25a-118">There are two ways that you can provide listener settings and security credentials:</span><span class="sxs-lookup"><span data-stu-id="7f25a-118">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="7f25a-119">Provide them directly in the service code:</span><span class="sxs-lookup"><span data-stu-id="7f25a-119">Provide them directly in the service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="7f25a-120">Provide them by using a [config package](service-fabric-application-and-service-manifests.md):</span><span class="sxs-lookup"><span data-stu-id="7f25a-120">Provide them by using a [config package](service-fabric-application-and-service-manifests.md):</span></span>

       <span data-ttu-id="7f25a-121">Add a named `TransportSettings` section in the settings.xml file.</span><span class="sxs-lookup"><span data-stu-id="7f25a-121">Add a named `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="7f25a-122">In this case, the `CreateServiceReplicaListeners` method will look like this:</span><span class="sxs-lookup"><span data-stu-id="7f25a-122">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="7f25a-123">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span><span class="sxs-lookup"><span data-stu-id="7f25a-123">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="7f25a-124">In this case, the `CreateServiceReplicaListeners` method will look like this:</span><span class="sxs-lookup"><span data-stu-id="7f25a-124">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="7f25a-125">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="7f25a-125">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="7f25a-126">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7f25a-126">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="7f25a-127">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span><span class="sxs-lookup"><span data-stu-id="7f25a-127">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="7f25a-128">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span><span class="sxs-lookup"><span data-stu-id="7f25a-128">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="7f25a-129">Make the following changes to the client code:</span><span class="sxs-lookup"><span data-stu-id="7f25a-129">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="7f25a-130">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span><span class="sxs-lookup"><span data-stu-id="7f25a-130">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="7f25a-131">Then create a TransportSettings section in that file.</span><span class="sxs-lookup"><span data-stu-id="7f25a-131">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="7f25a-132">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span><span class="sxs-lookup"><span data-stu-id="7f25a-132">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="7f25a-133">In that case, the earlier code is even further simplified:</span><span class="sxs-lookup"><span data-stu-id="7f25a-133">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```


<span data-ttu-id="7f25a-134">As a next step, read [Web API with OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="7f25a-134">As a next step, read [Web API with OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md).</span></span>
