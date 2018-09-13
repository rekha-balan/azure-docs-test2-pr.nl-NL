---
title: Load balance containers in Azure DC/OS cluster | Microsoft Docs
description: Load balance across multiple containers in an Azure Container Service DC/OS cluster.
services: container-service
documentationcenter: ''
author: rgardler
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, Micro-services, DC/OS, Azure
ms.assetid: f0ab5645-2636-42de-b23b-4c3a7e3aa8bb
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2016
ms.author: rogardle
ms.openlocfilehash: 2141ff9e3f756bad60c5cebc800e36ba3b6861ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564612"
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="8394e-104">Load balance containers in an Azure Container Service DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="8394e-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="8394e-105">In this article, we'll explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="8394e-105">In this article, we'll explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="8394e-106">This will enable you to scale your applications horizontally.</span><span class="sxs-lookup"><span data-stu-id="8394e-106">This will enable you to scale your applications horizontally.</span></span> <span data-ttu-id="8394e-107">It will also enable you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span><span class="sxs-lookup"><span data-stu-id="8394e-107">It will also enable you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8394e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8394e-108">Prerequisites</span></span>
<span data-ttu-id="8394e-109">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and [ensure that your client can connect to your cluster](container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8394e-109">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and [ensure that your client can connect to your cluster](container-service-connect.md).</span></span> 

## <a name="load-balancing"></a><span data-ttu-id="8394e-110">Load balancing</span><span class="sxs-lookup"><span data-stu-id="8394e-110">Load balancing</span></span>
<span data-ttu-id="8394e-111">There are two load-balancing layers in the Container Service cluster we will build:</span><span class="sxs-lookup"><span data-stu-id="8394e-111">There are two load-balancing layers in the Container Service cluster we will build:</span></span> 

1. <span data-ttu-id="8394e-112">Azure Load Balancer provides public entry points (the ones that end users will hit).</span><span class="sxs-lookup"><span data-stu-id="8394e-112">Azure Load Balancer provides public entry points (the ones that end users will hit).</span></span> <span data-ttu-id="8394e-113">This is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span><span class="sxs-lookup"><span data-stu-id="8394e-113">This is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>
2. <span data-ttu-id="8394e-114">The Marathon Load Balancer (marathon-lb) routes inbound requests to container instances that service those requests.</span><span class="sxs-lookup"><span data-stu-id="8394e-114">The Marathon Load Balancer (marathon-lb) routes inbound requests to container instances that service those requests.</span></span> <span data-ttu-id="8394e-115">As we scale the containers providing our web service, marathon-lb dynamically adapts.</span><span class="sxs-lookup"><span data-stu-id="8394e-115">As we scale the containers providing our web service, marathon-lb dynamically adapts.</span></span> <span data-ttu-id="8394e-116">This load balancer is not provided by default in your Container Service, but it is very easy to install.</span><span class="sxs-lookup"><span data-stu-id="8394e-116">This load balancer is not provided by default in your Container Service, but it is very easy to install.</span></span>

## <a name="marathon-load-balancer"></a><span data-ttu-id="8394e-117">Marathon Load Balancer</span><span class="sxs-lookup"><span data-stu-id="8394e-117">Marathon Load Balancer</span></span>
<span data-ttu-id="8394e-118">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span><span class="sxs-lookup"><span data-stu-id="8394e-118">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="8394e-119">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos will simply restart the container elsewhere and marathon-lb will adapt.</span><span class="sxs-lookup"><span data-stu-id="8394e-119">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos will simply restart the container elsewhere and marathon-lb will adapt.</span></span>

<span data-ttu-id="8394e-120">To install the Marathon Load Balancer you can use either the DC/OS web UI or the command line.</span><span class="sxs-lookup"><span data-stu-id="8394e-120">To install the Marathon Load Balancer you can use either the DC/OS web UI or the command line.</span></span>

### <a name="install-marathon-lb-using-dcos-web-ui"></a><span data-ttu-id="8394e-121">Install Marathon-LB using DC/OS Web UI</span><span class="sxs-lookup"><span data-stu-id="8394e-121">Install Marathon-LB using DC/OS Web UI</span></span>
1. <span data-ttu-id="8394e-122">Click 'Universe'</span><span class="sxs-lookup"><span data-stu-id="8394e-122">Click 'Universe'</span></span>
2. <span data-ttu-id="8394e-123">Search for 'Marathon-LB'</span><span class="sxs-lookup"><span data-stu-id="8394e-123">Search for 'Marathon-LB'</span></span>
3. <span data-ttu-id="8394e-124">Click 'Install'</span><span class="sxs-lookup"><span data-stu-id="8394e-124">Click 'Install'</span></span>

![Installing marathon-lb via the DC/OS Web Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/dcos/marathon-lb-install.png)

### <a name="install-marathon-lb-using-the-dcos-cli"></a><span data-ttu-id="8394e-126">Install Marathon-LB using the DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="8394e-126">Install Marathon-LB using the DC/OS CLI</span></span>
<span data-ttu-id="8394e-127">After installing the DC/OS CLI and ensuring you can connect to your cluster, run the following command from your client machine:</span><span class="sxs-lookup"><span data-stu-id="8394e-127">After installing the DC/OS CLI and ensuring you can connect to your cluster, run the following command from your client machine:</span></span>

```bash
dcos package install marathon-lb
```

<span data-ttu-id="8394e-128">This command automatically installs the load balancer on the public agents cluster.</span><span class="sxs-lookup"><span data-stu-id="8394e-128">This command automatically installs the load balancer on the public agents cluster.</span></span>

## <a name="deploy-a-load-balanced-web-application"></a><span data-ttu-id="8394e-129">Deploy A Load Balanced Web Application</span><span class="sxs-lookup"><span data-stu-id="8394e-129">Deploy A Load Balanced Web Application</span></span>
<span data-ttu-id="8394e-130">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span><span class="sxs-lookup"><span data-stu-id="8394e-130">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> <span data-ttu-id="8394e-131">For this example we will deploy a simple web server by using the following configuration:</span><span class="sxs-lookup"><span data-stu-id="8394e-131">For this example we will deploy a simple web server by using the following configuration:</span></span>

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}

```

* <span data-ttu-id="8394e-132">Set the value of `HAPROXY_0_VHOST` to the FQDN of the load balancer for your agents.</span><span class="sxs-lookup"><span data-stu-id="8394e-132">Set the value of `HAPROXY_0_VHOST` to the FQDN of the load balancer for your agents.</span></span> <span data-ttu-id="8394e-133">This is in the form `<acsName>agents.<region>.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8394e-133">This is in the form `<acsName>agents.<region>.cloudapp.azure.com`.</span></span> <span data-ttu-id="8394e-134">For example, if you create a Container Service cluster with name `myacs` in region `West US`, the FQDN would be `myacsagents.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8394e-134">For example, if you create a Container Service cluster with name `myacs` in region `West US`, the FQDN would be `myacsagents.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="8394e-135">You can also find this by looking for the load balancer with "agent" in the name when you're looking through the resources in the resource group that you created for Container Service in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8394e-135">You can also find this by looking for the load balancer with "agent" in the name when you're looking through the resources in the resource group that you created for Container Service in the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="8394e-136">Set the `servicePort` to a port >= 10,000.</span><span class="sxs-lookup"><span data-stu-id="8394e-136">Set the `servicePort` to a port >= 10,000.</span></span> <span data-ttu-id="8394e-137">This identifies the service that is being run in this container--marathon-lb uses this to identify services that it should balance across.</span><span class="sxs-lookup"><span data-stu-id="8394e-137">This identifies the service that is being run in this container--marathon-lb uses this to identify services that it should balance across.</span></span>
* <span data-ttu-id="8394e-138">Set the `HAPROXY_GROUP` label to "external".</span><span class="sxs-lookup"><span data-stu-id="8394e-138">Set the `HAPROXY_GROUP` label to "external".</span></span>
* <span data-ttu-id="8394e-139">Set `hostPort` to 0.</span><span class="sxs-lookup"><span data-stu-id="8394e-139">Set `hostPort` to 0.</span></span> <span data-ttu-id="8394e-140">This means that Marathon will arbitrarily allocate an available port.</span><span class="sxs-lookup"><span data-stu-id="8394e-140">This means that Marathon will arbitrarily allocate an available port.</span></span>
* <span data-ttu-id="8394e-141">Set `instances` to the number of instances you want to create.</span><span class="sxs-lookup"><span data-stu-id="8394e-141">Set `instances` to the number of instances you want to create.</span></span> <span data-ttu-id="8394e-142">You can always scale these up and down later.</span><span class="sxs-lookup"><span data-stu-id="8394e-142">You can always scale these up and down later.</span></span>

<span data-ttu-id="8394e-143">It is worth noting that by default Marathon will deploy to the private cluster, this means that the above deployment will only be accessible via your load balancer, which is usually the behavior we desire.</span><span class="sxs-lookup"><span data-stu-id="8394e-143">It is worth noting that by default Marathon will deploy to the private cluster, this means that the above deployment will only be accessible via your load balancer, which is usually the behavior we desire.</span></span>

### <a name="deploy-using-the-dcos-web-ui"></a><span data-ttu-id="8394e-144">Deploy using the DC/OS Web UI</span><span class="sxs-lookup"><span data-stu-id="8394e-144">Deploy using the DC/OS Web UI</span></span>
1. <span data-ttu-id="8394e-145">Visit the Marathon page at http://localhost/marathon (after setting up your [SSH tunnel](container-service-connect.md)) and click `Create Application`</span><span class="sxs-lookup"><span data-stu-id="8394e-145">Visit the Marathon page at http://localhost/marathon (after setting up your [SSH tunnel](container-service-connect.md)) and click `Create Application`</span></span>
2. <span data-ttu-id="8394e-146">In the `New Application` dialog click `JSON Mode` in the upper right corner</span><span class="sxs-lookup"><span data-stu-id="8394e-146">In the `New Application` dialog click `JSON Mode` in the upper right corner</span></span>
3. <span data-ttu-id="8394e-147">Paste the above JSON into the editor</span><span class="sxs-lookup"><span data-stu-id="8394e-147">Paste the above JSON into the editor</span></span>
4. <span data-ttu-id="8394e-148">Click `Create Application`</span><span class="sxs-lookup"><span data-stu-id="8394e-148">Click `Create Application`</span></span>

### <a name="deploy-using-the-dcos-cli"></a><span data-ttu-id="8394e-149">Deploy using the DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="8394e-149">Deploy using the DC/OS CLI</span></span>
<span data-ttu-id="8394e-150">To deploy this application with the DC/OS CLI simply copy the above JSON into a file called `hello-web.json`, and run:</span><span class="sxs-lookup"><span data-stu-id="8394e-150">To deploy this application with the DC/OS CLI simply copy the above JSON into a file called `hello-web.json`, and run:</span></span>

```bash
dcos marathon app add hello-web.json
```

## <a name="azure-load-balancer"></a><span data-ttu-id="8394e-151">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="8394e-151">Azure Load Balancer</span></span>
<span data-ttu-id="8394e-152">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span><span class="sxs-lookup"><span data-stu-id="8394e-152">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="8394e-153">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span><span class="sxs-lookup"><span data-stu-id="8394e-153">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="8394e-154">You should be able to hit your agent load balancer's FQDN--and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span><span class="sxs-lookup"><span data-stu-id="8394e-154">You should be able to hit your agent load balancer's FQDN--and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> <span data-ttu-id="8394e-155">However, if you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span><span class="sxs-lookup"><span data-stu-id="8394e-155">However, if you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="8394e-156">You can do this from the [Azure CLI](../xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="8394e-156">You can do this from the [Azure CLI](../xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span> <span data-ttu-id="8394e-157">You can also do this using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8394e-157">You can also do this using the Azure Portal.</span></span>

## <a name="additional-scenarios"></a><span data-ttu-id="8394e-158">Additional scenarios</span><span class="sxs-lookup"><span data-stu-id="8394e-158">Additional scenarios</span></span>
<span data-ttu-id="8394e-159">You could have a scenario where you use different domains to expose different services.</span><span class="sxs-lookup"><span data-stu-id="8394e-159">You could have a scenario where you use different domains to expose different services.</span></span> <span data-ttu-id="8394e-160">For example:</span><span class="sxs-lookup"><span data-stu-id="8394e-160">For example:</span></span>

<span data-ttu-id="8394e-161">mydomain1.com -> Azure LB:80 -> marathon-lb:10001 -> mycontainer1:33292</span><span class="sxs-lookup"><span data-stu-id="8394e-161">mydomain1.com -> Azure LB:80 -> marathon-lb:10001 -> mycontainer1:33292</span></span>  
<span data-ttu-id="8394e-162">mydomain2.com -> Azure LB:80 -> marathon-lb:10002 -> mycontainer2:22321</span><span class="sxs-lookup"><span data-stu-id="8394e-162">mydomain2.com -> Azure LB:80 -> marathon-lb:10002 -> mycontainer2:22321</span></span>

<span data-ttu-id="8394e-163">To achieve this, check out [virtual hosts](https://mesosphere.com/blog/2015/12/04/dcos-marathon-lb/), which provide a way to associate domains to specific marathon-lb paths.</span><span class="sxs-lookup"><span data-stu-id="8394e-163">To achieve this, check out [virtual hosts](https://mesosphere.com/blog/2015/12/04/dcos-marathon-lb/), which provide a way to associate domains to specific marathon-lb paths.</span></span>

<span data-ttu-id="8394e-164">Alternatively, you could expose different ports and remap them to the correct service behind marathon-lb. For example:</span><span class="sxs-lookup"><span data-stu-id="8394e-164">Alternatively, you could expose different ports and remap them to the correct service behind marathon-lb. For example:</span></span>

<span data-ttu-id="8394e-165">Azure lb:80 -> marathon-lb:10001 -> mycontainer:233423</span><span class="sxs-lookup"><span data-stu-id="8394e-165">Azure lb:80 -> marathon-lb:10001 -> mycontainer:233423</span></span>  
<span data-ttu-id="8394e-166">Azure lb:8080 -> marathon-lb:1002 -> mycontainer2:33432</span><span class="sxs-lookup"><span data-stu-id="8394e-166">Azure lb:8080 -> marathon-lb:1002 -> mycontainer2:33432</span></span>

## <a name="next-steps"></a><span data-ttu-id="8394e-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="8394e-167">Next steps</span></span>
<span data-ttu-id="8394e-168">See the DC/OS documentation for more on [marathon-lb](https://dcos.io/docs/1.7/usage/service-discovery/marathon-lb/).</span><span class="sxs-lookup"><span data-stu-id="8394e-168">See the DC/OS documentation for more on [marathon-lb](https://dcos.io/docs/1.7/usage/service-discovery/marathon-lb/).</span></span>


