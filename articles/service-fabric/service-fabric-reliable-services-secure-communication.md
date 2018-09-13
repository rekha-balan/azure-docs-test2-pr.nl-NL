---
title: Help secure communication for services in Azure Service Fabric | Microsoft Docs
description: Overview of how to help secure communication for reliable services that are running in an Azure Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/05/2017
ms.author: suchia
ms.openlocfilehash: 89eca322062f5e5c51142b2cc9e758004583cb3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564697"
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="07cb4-103">Help secure communication for services in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07cb4-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java on Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="07cb4-106">Security is one of the most important aspects of communication.</span><span class="sxs-lookup"><span data-stu-id="07cb4-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="07cb4-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span><span class="sxs-lookup"><span data-stu-id="07cb4-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="07cb4-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span><span class="sxs-lookup"><span data-stu-id="07cb4-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="07cb4-109">Help secure a service when you're using service remoting</span><span class="sxs-lookup"><span data-stu-id="07cb4-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="07cb4-110">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span><span class="sxs-lookup"><span data-stu-id="07cb4-110">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="07cb4-111">To help secure a service when you're using service remoting, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="07cb4-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="07cb4-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span><span class="sxs-lookup"><span data-stu-id="07cb4-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="07cb4-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span><span class="sxs-lookup"><span data-stu-id="07cb4-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="07cb4-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span><span class="sxs-lookup"><span data-stu-id="07cb4-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="07cb4-115">Add listener settings and security credentials.</span><span class="sxs-lookup"><span data-stu-id="07cb4-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="07cb4-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="07cb4-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="07cb4-117">There are two ways that you can provide listener settings and security credentials:</span><span class="sxs-lookup"><span data-stu-id="07cb4-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="07cb4-118">Provide them directly in the service code:</span><span class="sxs-lookup"><span data-stu-id="07cb4-118">Provide them directly in the service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportListenerSettings listenerSettings = new FabricTransportListenerSettings
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
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="07cb4-119">Provide them by using a [config package](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="07cb4-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="07cb4-120">Add a `TransportSettings` section in the settings.xml file.</span><span class="sxs-lookup"><span data-stu-id="07cb4-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateful".-->
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="07cb4-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span><span class="sxs-lookup"><span data-stu-id="07cb4-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportListenerSettings.LoadFrom("HelloWorldStateful")))
           };
       }
       ```

        <span data-ttu-id="07cb4-122">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span><span class="sxs-lookup"><span data-stu-id="07cb4-122">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="07cb4-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span><span class="sxs-lookup"><span data-stu-id="07cb4-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="07cb4-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="07cb4-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="07cb4-125">Pass in `FabricTransportSettings`, which contains `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="07cb4-125">Pass in `FabricTransportSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");

    FabricTransportSettings transportSettings = new FabricTransportSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="07cb4-126">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span><span class="sxs-lookup"><span data-stu-id="07cb4-126">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="07cb4-127">Create a TransportSettings section that is similar to the service code, as shown earlier.</span><span class="sxs-lookup"><span data-stu-id="07cb4-127">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="07cb4-128">Make the following changes to the client code:</span><span class="sxs-lookup"><span data-stu-id="07cb4-128">Make the following changes to the client code:</span></span>

    ```csharp

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportSettings.LoadFrom("TransportSettingsPrefix")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="07cb4-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span><span class="sxs-lookup"><span data-stu-id="07cb4-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="07cb4-130">Then create a TransportSettings section in that file.</span><span class="sxs-lookup"><span data-stu-id="07cb4-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="07cb4-131">Similar to the service, if you add a `TransportSettings` section without any prefix in client settings.xml/client_name.settings.xml, `FabricTransportSettings` will load all the settings from this section by default.</span><span class="sxs-lookup"><span data-stu-id="07cb4-131">Similar to the service, if you add a `TransportSettings` section without any prefix in client settings.xml/client_name.settings.xml, `FabricTransportSettings` will load all the settings from this section by default.</span></span>

    <span data-ttu-id="07cb4-132">In that case, the earlier code is even further simplified:</span><span class="sxs-lookup"><span data-stu-id="07cb4-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="07cb4-133">Help secure a service when you're using a WCF-based communication stack</span><span class="sxs-lookup"><span data-stu-id="07cb4-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="07cb4-134">We'll be using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span><span class="sxs-lookup"><span data-stu-id="07cb4-134">We'll be using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="07cb4-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="07cb4-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="07cb4-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span><span class="sxs-lookup"><span data-stu-id="07cb4-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="07cb4-137">To do this, modify the `CreateServiceReplicaListeners` method.</span><span class="sxs-lookup"><span data-stu-id="07cb4-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in the ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="07cb4-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span><span class="sxs-lookup"><span data-stu-id="07cb4-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="07cb4-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="07cb4-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="07cb4-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="07cb4-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="07cb4-141">Use the client to invoke service methods.</span><span class="sxs-lookup"><span data-stu-id="07cb4-141">Use the client to invoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="07cb4-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="07cb4-142">Next steps</span></span>
* [<span data-ttu-id="07cb4-143">Web API with OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="07cb4-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
