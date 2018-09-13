---
title: Load balance containers in Azure DC/OS cluster
description: Load balance across multiple containers in an Azure Container Service DC/OS cluster.
services: container-service
author: rgardler
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 7e71b279d6681696b8666846cfbd27007f464679
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866978"
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="11186-103">Load balance containers in an Azure Container Service DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="11186-103">Load balance containers in an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="11186-104">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="11186-104">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="11186-105">This configuration enables you to scale your applications horizontally.</span><span class="sxs-lookup"><span data-stu-id="11186-105">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="11186-106">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span><span class="sxs-lookup"><span data-stu-id="11186-106">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="11186-107">In this tutorial, you:</span><span class="sxs-lookup"><span data-stu-id="11186-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="11186-108">Configure a Marathon Load Balancer</span><span class="sxs-lookup"><span data-stu-id="11186-108">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="11186-109">Deploy an application using the load balancer</span><span class="sxs-lookup"><span data-stu-id="11186-109">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="11186-110">Configure and Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="11186-110">Configure and Azure load balancer</span></span>

<span data-ttu-id="11186-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="11186-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="11186-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span><span class="sxs-lookup"><span data-stu-id="11186-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="11186-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="11186-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="11186-114">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="11186-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="11186-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="11186-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="11186-116">Load balancing overview</span><span class="sxs-lookup"><span data-stu-id="11186-116">Load balancing overview</span></span>

<span data-ttu-id="11186-117">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span><span class="sxs-lookup"><span data-stu-id="11186-117">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="11186-118">**Azure Load Balancer** provides public entry points (the ones that end users access).</span><span class="sxs-lookup"><span data-stu-id="11186-118">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="11186-119">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span><span class="sxs-lookup"><span data-stu-id="11186-119">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="11186-120">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span><span class="sxs-lookup"><span data-stu-id="11186-120">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="11186-121">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span><span class="sxs-lookup"><span data-stu-id="11186-121">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="11186-122">This load balancer is not provided by default in your Container Service, but it is easy to install.</span><span class="sxs-lookup"><span data-stu-id="11186-122">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="11186-123">Configure Marathon Load Balancer</span><span class="sxs-lookup"><span data-stu-id="11186-123">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="11186-124">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span><span class="sxs-lookup"><span data-stu-id="11186-124">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="11186-125">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span><span class="sxs-lookup"><span data-stu-id="11186-125">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="11186-126">Run the following command to install the marathon load balancer on the public agent's cluster.</span><span class="sxs-lookup"><span data-stu-id="11186-126">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="11186-127">Deploy load balanced application</span><span class="sxs-lookup"><span data-stu-id="11186-127">Deploy load balanced application</span></span>

<span data-ttu-id="11186-128">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span><span class="sxs-lookup"><span data-stu-id="11186-128">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="11186-129">First, get the FQDN of the publicly exposed agents.</span><span class="sxs-lookup"><span data-stu-id="11186-129">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="11186-130">Next, create a file named *hello-web.json* and copy in the following contents.</span><span class="sxs-lookup"><span data-stu-id="11186-130">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="11186-131">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span><span class="sxs-lookup"><span data-stu-id="11186-131">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

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

<span data-ttu-id="11186-132">Use the DC/OS CLI to run the application.</span><span class="sxs-lookup"><span data-stu-id="11186-132">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="11186-133">By default Marathon deploys the applicaton to the private cluster.</span><span class="sxs-lookup"><span data-stu-id="11186-133">By default Marathon deploys the applicaton to the private cluster.</span></span> <span data-ttu-id="11186-134">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span><span class="sxs-lookup"><span data-stu-id="11186-134">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="11186-135">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span><span class="sxs-lookup"><span data-stu-id="11186-135">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Image of load balanced application](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="11186-137">Configure Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="11186-137">Configure Azure Load Balancer</span></span>

<span data-ttu-id="11186-138">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span><span class="sxs-lookup"><span data-stu-id="11186-138">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="11186-139">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span><span class="sxs-lookup"><span data-stu-id="11186-139">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="11186-140">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span><span class="sxs-lookup"><span data-stu-id="11186-140">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="11186-141">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span><span class="sxs-lookup"><span data-stu-id="11186-141">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="11186-142">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="11186-142">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11186-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="11186-143">Next steps</span></span>

<span data-ttu-id="11186-144">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span><span class="sxs-lookup"><span data-stu-id="11186-144">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="11186-145">Configure a Marathon Load Balancer</span><span class="sxs-lookup"><span data-stu-id="11186-145">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="11186-146">Deploy an application using the load balancer</span><span class="sxs-lookup"><span data-stu-id="11186-146">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="11186-147">Configure and Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="11186-147">Configure and Azure load balancer</span></span>

<span data-ttu-id="11186-148">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span><span class="sxs-lookup"><span data-stu-id="11186-148">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11186-149">Mount Azure File Share in DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="11186-149">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)