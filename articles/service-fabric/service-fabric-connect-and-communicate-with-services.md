---
title: Connect and communicate with services in Azure Service Fabric | Microsoft Docs
description: Learn how to resolve, connect, and communicate with services in Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/01/2017
ms.author: vturecek
ms.openlocfilehash: bc20e3e488b866eb519a6ddc2c6fbd7cc090236f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828269"
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="58e9f-103">Connect and communicate with services in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="58e9f-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="58e9f-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="58e9f-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="58e9f-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="58e9f-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="58e9f-106">Services are not statically tied to a particular machine or address.</span><span class="sxs-lookup"><span data-stu-id="58e9f-106">Services are not statically tied to a particular machine or address.</span></span>

<span data-ttu-id="58e9f-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span><span class="sxs-lookup"><span data-stu-id="58e9f-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="58e9f-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span><span class="sxs-lookup"><span data-stu-id="58e9f-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="58e9f-109">There are also client applications that connect to and communicate with services.</span><span class="sxs-lookup"><span data-stu-id="58e9f-109">There are also client applications that connect to and communicate with services.</span></span> <span data-ttu-id="58e9f-110">This document discusses how to set up communication with and between your services in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="58e9f-110">This document discusses how to set up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="58e9f-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="58e9f-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="58e9f-112">Bring your own protocol</span><span class="sxs-lookup"><span data-stu-id="58e9f-112">Bring your own protocol</span></span>
<span data-ttu-id="58e9f-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span><span class="sxs-lookup"><span data-stu-id="58e9f-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="58e9f-114">This includes communication.</span><span class="sxs-lookup"><span data-stu-id="58e9f-114">This includes communication.</span></span> <span data-ttu-id="58e9f-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span><span class="sxs-lookup"><span data-stu-id="58e9f-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="58e9f-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span><span class="sxs-lookup"><span data-stu-id="58e9f-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="58e9f-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span><span class="sxs-lookup"><span data-stu-id="58e9f-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span></span> <span data-ttu-id="58e9f-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span><span class="sxs-lookup"><span data-stu-id="58e9f-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![service endpoints][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="58e9f-120">Service discovery and resolution</span><span class="sxs-lookup"><span data-stu-id="58e9f-120">Service discovery and resolution</span></span>
<span data-ttu-id="58e9f-121">In a distributed system, services may move from one machine to another over time.</span><span class="sxs-lookup"><span data-stu-id="58e9f-121">In a distributed system, services may move from one machine to another over time.</span></span> <span data-ttu-id="58e9f-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span><span class="sxs-lookup"><span data-stu-id="58e9f-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span></span>

![Distribution of services][7]

<span data-ttu-id="58e9f-124">Service Fabric provides a discovery and resolution service called the Naming Service.</span><span class="sxs-lookup"><span data-stu-id="58e9f-124">Service Fabric provides a discovery and resolution service called the Naming Service.</span></span> <span data-ttu-id="58e9f-125">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span><span class="sxs-lookup"><span data-stu-id="58e9f-125">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span></span> <span data-ttu-id="58e9f-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="58e9f-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="58e9f-127">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span><span class="sxs-lookup"><span data-stu-id="58e9f-127">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span></span> <span data-ttu-id="58e9f-128">This is analogous to websites that have constant URLs but where the IP address may change.</span><span class="sxs-lookup"><span data-stu-id="58e9f-128">This is analogous to websites that have constant URLs but where the IP address may change.</span></span> <span data-ttu-id="58e9f-129">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span><span class="sxs-lookup"><span data-stu-id="58e9f-129">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span></span>

![service endpoints][2]

<span data-ttu-id="58e9f-131">Resolving and connecting to services involves the following steps run in a loop:</span><span class="sxs-lookup"><span data-stu-id="58e9f-131">Resolving and connecting to services involves the following steps run in a loop:</span></span>

* <span data-ttu-id="58e9f-132">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span><span class="sxs-lookup"><span data-stu-id="58e9f-132">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span></span>
* <span data-ttu-id="58e9f-133">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span><span class="sxs-lookup"><span data-stu-id="58e9f-133">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="58e9f-134">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span><span class="sxs-lookup"><span data-stu-id="58e9f-134">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span></span> <span data-ttu-id="58e9f-135">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span><span class="sxs-lookup"><span data-stu-id="58e9f-135">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span></span>

## <a name="connecting-to-other-services"></a><span data-ttu-id="58e9f-136">Connecting to other services</span><span class="sxs-lookup"><span data-stu-id="58e9f-136">Connecting to other services</span></span>
<span data-ttu-id="58e9f-137">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span><span class="sxs-lookup"><span data-stu-id="58e9f-137">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="58e9f-138">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span><span class="sxs-lookup"><span data-stu-id="58e9f-138">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span></span> <span data-ttu-id="58e9f-139">A DNS service and a reverse proxy service.</span><span class="sxs-lookup"><span data-stu-id="58e9f-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="58e9f-140">DNS service</span><span class="sxs-lookup"><span data-stu-id="58e9f-140">DNS service</span></span>
<span data-ttu-id="58e9f-141">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span><span class="sxs-lookup"><span data-stu-id="58e9f-141">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="58e9f-142">This is exactly what the DNS service does.</span><span class="sxs-lookup"><span data-stu-id="58e9f-142">This is exactly what the DNS service does.</span></span> <span data-ttu-id="58e9f-143">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span><span class="sxs-lookup"><span data-stu-id="58e9f-143">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="58e9f-144">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span><span class="sxs-lookup"><span data-stu-id="58e9f-144">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span></span> <span data-ttu-id="58e9f-145">The DNS name for the service is provided at the time of creation.</span><span class="sxs-lookup"><span data-stu-id="58e9f-145">The DNS name for the service is provided at the time of creation.</span></span> 

![service endpoints][9]

<span data-ttu-id="58e9f-147">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span><span class="sxs-lookup"><span data-stu-id="58e9f-147">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="58e9f-148">Reverse proxy service</span><span class="sxs-lookup"><span data-stu-id="58e9f-148">Reverse proxy service</span></span>
<span data-ttu-id="58e9f-149">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span><span class="sxs-lookup"><span data-stu-id="58e9f-149">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="58e9f-150">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Service.</span><span class="sxs-lookup"><span data-stu-id="58e9f-150">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Service.</span></span> <span data-ttu-id="58e9f-151">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span><span class="sxs-lookup"><span data-stu-id="58e9f-151">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![service endpoints][10]

<span data-ttu-id="58e9f-153">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span><span class="sxs-lookup"><span data-stu-id="58e9f-153">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="58e9f-154">Connections from external clients</span><span class="sxs-lookup"><span data-stu-id="58e9f-154">Connections from external clients</span></span>
<span data-ttu-id="58e9f-155">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span><span class="sxs-lookup"><span data-stu-id="58e9f-155">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="58e9f-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span><span class="sxs-lookup"><span data-stu-id="58e9f-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="58e9f-157">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span><span class="sxs-lookup"><span data-stu-id="58e9f-157">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="58e9f-158">Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="58e9f-158">Service Fabric in Azure</span></span>
<span data-ttu-id="58e9f-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="58e9f-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="58e9f-160">All external traffic to the cluster must pass through the load balancer.</span><span class="sxs-lookup"><span data-stu-id="58e9f-160">All external traffic to the cluster must pass through the load balancer.</span></span> <span data-ttu-id="58e9f-161">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span><span class="sxs-lookup"><span data-stu-id="58e9f-161">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span></span> <span data-ttu-id="58e9f-162">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span><span class="sxs-lookup"><span data-stu-id="58e9f-162">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure Load Balancer and Service Fabric topology][3]

<span data-ttu-id="58e9f-164">For example, in order to accept external traffic on port **80**, the following things must be configured:</span><span class="sxs-lookup"><span data-stu-id="58e9f-164">For example, in order to accept external traffic on port **80**, the following things must be configured:</span></span>

1. <span data-ttu-id="58e9f-165">Write a service that listens on port 80.</span><span class="sxs-lookup"><span data-stu-id="58e9f-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="58e9f-166">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span><span class="sxs-lookup"><span data-stu-id="58e9f-166">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="58e9f-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span><span class="sxs-lookup"><span data-stu-id="58e9f-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span></span> <span data-ttu-id="58e9f-168">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span><span class="sxs-lookup"><span data-stu-id="58e9f-168">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span></span>

    ![Open a port on a node type][4]
3. <span data-ttu-id="58e9f-170">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="58e9f-170">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span></span> <span data-ttu-id="58e9f-171">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span><span class="sxs-lookup"><span data-stu-id="58e9f-171">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Forward traffic in the Azure Load Balancer][5]
4. <span data-ttu-id="58e9f-173">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span><span class="sxs-lookup"><span data-stu-id="58e9f-173">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span></span> <span data-ttu-id="58e9f-174">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span><span class="sxs-lookup"><span data-stu-id="58e9f-174">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span></span> <span data-ttu-id="58e9f-175">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span><span class="sxs-lookup"><span data-stu-id="58e9f-175">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span></span> <span data-ttu-id="58e9f-176">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span><span class="sxs-lookup"><span data-stu-id="58e9f-176">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Forward traffic in the Azure Load Balancer][8]

<span data-ttu-id="58e9f-178">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span><span class="sxs-lookup"><span data-stu-id="58e9f-178">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span></span> <span data-ttu-id="58e9f-179">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span><span class="sxs-lookup"><span data-stu-id="58e9f-179">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="58e9f-180">Reliable Services: Built-in communication API options</span><span class="sxs-lookup"><span data-stu-id="58e9f-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="58e9f-181">The Reliable Services framework ships with several pre-built communication options.</span><span class="sxs-lookup"><span data-stu-id="58e9f-181">The Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="58e9f-182">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span><span class="sxs-lookup"><span data-stu-id="58e9f-182">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span></span>

* <span data-ttu-id="58e9f-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="58e9f-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="58e9f-184">This is the easiest and fastest way to get started with service communication.</span><span class="sxs-lookup"><span data-stu-id="58e9f-184">This is the easiest and fastest way to get started with service communication.</span></span> <span data-ttu-id="58e9f-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span><span class="sxs-lookup"><span data-stu-id="58e9f-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="58e9f-186">This is available for both C# and Java applications.</span><span class="sxs-lookup"><span data-stu-id="58e9f-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="58e9f-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="58e9f-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="58e9f-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span><span class="sxs-lookup"><span data-stu-id="58e9f-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="58e9f-189">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="58e9f-189">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="58e9f-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span><span class="sxs-lookup"><span data-stu-id="58e9f-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span></span> <span data-ttu-id="58e9f-191">This however is only available for C# applications on Windows based clusters.</span><span class="sxs-lookup"><span data-stu-id="58e9f-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="58e9f-192">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="58e9f-192">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="58e9f-193">Using custom protocols and other communication frameworks</span><span class="sxs-lookup"><span data-stu-id="58e9f-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="58e9f-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="58e9f-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="58e9f-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span><span class="sxs-lookup"><span data-stu-id="58e9f-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span></span> <span data-ttu-id="58e9f-196">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="58e9f-196">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58e9f-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="58e9f-197">Next steps</span></span>
<span data-ttu-id="58e9f-198">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="58e9f-198">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
