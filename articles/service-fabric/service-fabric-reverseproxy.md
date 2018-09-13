---
title: Azure Service Fabric reverse proxy | Microsoft Docs
description: Use Service Fabric's reverse proxy for communication to microservices from inside and outside the cluster.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: bharatn
ms.openlocfilehash: e43a6265b891003a8099d52f27af89d020a8cf6c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548788"
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="9b9ef-103">Reverse proxy in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b9ef-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="9b9ef-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="9b9ef-105">Microservices communication model</span><span class="sxs-lookup"><span data-stu-id="9b9ef-105">Microservices communication model</span></span>
<span data-ttu-id="9b9ef-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="9b9ef-107">So, the endpoints for microservices can change dynamically.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="9b9ef-108">The typical pattern to communicate to the microservice is the following resolve loop:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="9b9ef-109">Resolve the service location initially through the naming service.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="9b9ef-110">Connect to the service.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-110">Connect to the service.</span></span>
3. <span data-ttu-id="9b9ef-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="9b9ef-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="9b9ef-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="9b9ef-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="9b9ef-114">Communicating by using the reverse proxy</span><span class="sxs-lookup"><span data-stu-id="9b9ef-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="9b9ef-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="9b9ef-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="9b9ef-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![Internal communication][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="9b9ef-119">Reaching microservices from outside the cluster</span><span class="sxs-lookup"><span data-stu-id="9b9ef-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="9b9ef-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="9b9ef-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="9b9ef-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="9b9ef-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="9b9ef-124">The microservices can move between nodes on failover.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="9b9ef-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="9b9ef-126">Reaching microservices via the reverse proxy from outside the cluster</span><span class="sxs-lookup"><span data-stu-id="9b9ef-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="9b9ef-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="9b9ef-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![External communication][0]

> [!WARNING]
> <span data-ttu-id="9b9ef-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="9b9ef-131">URI format for addressing services by using the reverse proxy</span><span class="sxs-lookup"><span data-stu-id="9b9ef-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="9b9ef-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="9b9ef-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="9b9ef-134">For HTTPS traffic, Secure Sockets Layer (SSL) termination occurs at the reverse proxy.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-134">For HTTPS traffic, Secure Sockets Layer (SSL) termination occurs at the reverse proxy.</span></span> <span data-ttu-id="9b9ef-135">The reverse proxy uses HTTP to forward requests to services in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-135">The reverse proxy uses HTTP to forward requests to services in the cluster.</span></span>

    <span data-ttu-id="9b9ef-136">Note that HTTPS services are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-136">Note that HTTPS services are not currently supported.</span></span>
* <span data-ttu-id="9b9ef-137">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-137">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com.</span></span> <span data-ttu-id="9b9ef-138">By default, the reverse proxy runs on every node.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-138">By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="9b9ef-139">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-139">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="9b9ef-140">**Port:** This is the port, such as 19008, that has been specified for the reverse proxy.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-140">**Port:** This is the port, such as 19008, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="9b9ef-141">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-141">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="9b9ef-142">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-142">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>
* <span data-ttu-id="9b9ef-143">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-143">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="9b9ef-144">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-144">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="9b9ef-145">Note that this is *not* the partition ID GUID.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-145">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="9b9ef-146">This parameter is not required for services that use the singleton partition scheme.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-146">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="9b9ef-147">**PartitionKind:** This is the service partition scheme.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-147">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="9b9ef-148">This can be 'Int64Range' or 'Named'.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-148">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="9b9ef-149">This parameter is not required for services that use the singleton partition scheme.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-149">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="9b9ef-150">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-150">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="9b9ef-151">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-151">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="9b9ef-152">This can be omitted if the service has only one listener.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-152">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="9b9ef-153">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-153">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="9b9ef-154">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-154">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="9b9ef-155">When this parameter is not specified, the default is 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-155">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="9b9ef-156">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-156">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="9b9ef-157">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-157">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="9b9ef-158">The default value is 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-158">The default value is 60 seconds.</span></span> <span data-ttu-id="9b9ef-159">This is an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-159">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="9b9ef-160">Example usage</span><span class="sxs-lookup"><span data-stu-id="9b9ef-160">Example usage</span></span>
<span data-ttu-id="9b9ef-161">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-161">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="9b9ef-162">Following are the resources for the service:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-162">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="9b9ef-163">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-163">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="9b9ef-164">Externally: `http://mycluster.eastus.cloudapp.azure.com:19008/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="9b9ef-164">Externally: `http://mycluster.eastus.cloudapp.azure.com:19008/MyApp/MyService`</span></span>
* <span data-ttu-id="9b9ef-165">Internally: `http://localhost:19008/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="9b9ef-165">Internally: `http://localhost:19008/MyApp/MyService`</span></span>

<span data-ttu-id="9b9ef-166">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-166">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="9b9ef-167">Externally: `http://mycluster.eastus.cloudapp.azure.com:19008/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="9b9ef-167">Externally: `http://mycluster.eastus.cloudapp.azure.com:19008/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="9b9ef-168">Internally: `http://localhost:19008/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="9b9ef-168">Internally: `http://localhost:19008/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="9b9ef-169">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-169">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="9b9ef-170">Externally: `http://mycluster.eastus.cloudapp.azure.com:19008/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="9b9ef-170">Externally: `http://mycluster.eastus.cloudapp.azure.com:19008/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="9b9ef-171">Internally: `http://localhost:19008/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="9b9ef-171">Internally: `http://localhost:19008/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="9b9ef-172">The gateway will then forward these requests to the service's URL:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-172">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="9b9ef-173">Special handling for port-sharing services</span><span class="sxs-lookup"><span data-stu-id="9b9ef-173">Special handling for port-sharing services</span></span>
<span data-ttu-id="9b9ef-174">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-174">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="9b9ef-175">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-175">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="9b9ef-176">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-176">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="9b9ef-177">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-177">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="9b9ef-178">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-178">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="9b9ef-179">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="9b9ef-179">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="9b9ef-180">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="9b9ef-180">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="9b9ef-181">Katana</span><span class="sxs-lookup"><span data-stu-id="9b9ef-181">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="9b9ef-182">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-182">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="9b9ef-183">In this case, the gateway will receive an HTTP 404 response from the web server.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-183">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="9b9ef-184">Thus, an HTTP 404 has two distinct meanings:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-184">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="9b9ef-185">Case #1: The service address is correct, but the resource that the user requested does not exist.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-185">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="9b9ef-186">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-186">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="9b9ef-187">The first case is a normal HTTP 404, which is considered a user error.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-187">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="9b9ef-188">However, in the second case, the user has requested a resource that does exist.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-188">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="9b9ef-189">Application Gateway was unable to locate it because the service itself has moved.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-189">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="9b9ef-190">Application Gateway needs to resolve the address again and retry the request.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-190">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="9b9ef-191">Application Gateway thus needs a way to distinguish between these two cases.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-191">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="9b9ef-192">To make that distinction, a hint from the server is required.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-192">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="9b9ef-193">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-193">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="9b9ef-194">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-194">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="9b9ef-195">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-195">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="9b9ef-196">Setup and configuration</span><span class="sxs-lookup"><span data-stu-id="9b9ef-196">Setup and configuration</span></span>
<span data-ttu-id="9b9ef-197">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-197">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="9b9ef-198">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-198">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="9b9ef-199">First, you get the template for the cluster that you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-199">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="9b9ef-200">You can either use the sample templates or create a custom Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-200">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="9b9ef-201">Then, you can enable the reverse proxy by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b9ef-201">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="9b9ef-202">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-202">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19008,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="9b9ef-203">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b9ef-203">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="9b9ef-204">The port is identified by the parameter name, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-204">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="9b9ef-205">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-205">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="9b9ef-206">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b9ef-206">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="9b9ef-207">Supporting a reverse proxy certificate that's different from the cluster certificate</span><span class="sxs-lookup"><span data-stu-id="9b9ef-207">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="9b9ef-208">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-208">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="9b9ef-209">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b9ef-209">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="9b9ef-210">For installation, add that certificate to the osProfile.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-210">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="9b9ef-211">The extension section of the template can update the certificate in the ACL.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-211">The extension section of the template can update the certificate in the ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="9b9ef-212">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-212">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="9b9ef-213">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span><span class="sxs-lookup"><span data-stu-id="9b9ef-213">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b9ef-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b9ef-214">Next steps</span></span>
* <span data-ttu-id="9b9ef-215">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9b9ef-215">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="9b9ef-216">Remote procedure calls with Reliable Services remoting</span><span class="sxs-lookup"><span data-stu-id="9b9ef-216">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="9b9ef-217">Web API that uses OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9b9ef-217">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="9b9ef-218">WCF communication by using Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9b9ef-218">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reverseproxy/external-communication.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reverseproxy/internal-communication.png


