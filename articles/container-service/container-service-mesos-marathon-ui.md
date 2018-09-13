---
title: Manage Azure DC/OS cluster with Marathon UI | Microsoft Docs
description: Deploy containers to an Azure Container Service cluster service by using the Marathon web UI.
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: d148ed1e-b582-4d51-944f-1ac7ae3c4fd6
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.openlocfilehash: add77a5d053d3236f27ba8c75470b8a206b775c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555220"
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="52f3f-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span><span class="sxs-lookup"><span data-stu-id="52f3f-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>
<span data-ttu-id="52f3f-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span><span class="sxs-lookup"><span data-stu-id="52f3f-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="52f3f-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span><span class="sxs-lookup"><span data-stu-id="52f3f-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="52f3f-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span><span class="sxs-lookup"><span data-stu-id="52f3f-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="52f3f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52f3f-108">Prerequisites</span></span>
<span data-ttu-id="52f3f-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="52f3f-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="52f3f-110">You also need to have remote connectivity to this cluster.</span><span class="sxs-lookup"><span data-stu-id="52f3f-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="52f3f-111">For more information on these items, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="52f3f-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="52f3f-112">Deploy an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="52f3f-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="52f3f-113">Connect to an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="52f3f-113">Connect to an Azure Container Service cluster</span></span>](container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="52f3f-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span><span class="sxs-lookup"><span data-stu-id="52f3f-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="52f3f-115">Explore the DC/OS UI</span><span class="sxs-lookup"><span data-stu-id="52f3f-115">Explore the DC/OS UI</span></span>
<span data-ttu-id="52f3f-116">With a Secure Shell (SSH) tunnel [established](container-service-connect.md), browse to http://localhost/.</span><span class="sxs-lookup"><span data-stu-id="52f3f-116">With a Secure Shell (SSH) tunnel [established](container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="52f3f-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span><span class="sxs-lookup"><span data-stu-id="52f3f-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="52f3f-119">Explore the Marathon UI</span><span class="sxs-lookup"><span data-stu-id="52f3f-119">Explore the Marathon UI</span></span>
<span data-ttu-id="52f3f-120">To see the Marathon UI, browse to http://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="52f3f-120">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="52f3f-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="52f3f-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="52f3f-122">You can also see information about running containers and applications.</span><span class="sxs-lookup"><span data-stu-id="52f3f-122">You can also see information about running containers and applications.</span></span>  

![Marathon UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="52f3f-124">Deploy a Docker-formatted container</span><span class="sxs-lookup"><span data-stu-id="52f3f-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="52f3f-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span><span class="sxs-lookup"><span data-stu-id="52f3f-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="52f3f-126">Field</span><span class="sxs-lookup"><span data-stu-id="52f3f-126">Field</span></span> | <span data-ttu-id="52f3f-127">Value</span><span class="sxs-lookup"><span data-stu-id="52f3f-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="52f3f-128">ID</span><span class="sxs-lookup"><span data-stu-id="52f3f-128">ID</span></span> |<span data-ttu-id="52f3f-129">nginx</span><span class="sxs-lookup"><span data-stu-id="52f3f-129">nginx</span></span> |
| <span data-ttu-id="52f3f-130">Memory</span><span class="sxs-lookup"><span data-stu-id="52f3f-130">Memory</span></span> | <span data-ttu-id="52f3f-131">32</span><span class="sxs-lookup"><span data-stu-id="52f3f-131">32</span></span> |
| <span data-ttu-id="52f3f-132">Image</span><span class="sxs-lookup"><span data-stu-id="52f3f-132">Image</span></span> |<span data-ttu-id="52f3f-133">nginx</span><span class="sxs-lookup"><span data-stu-id="52f3f-133">nginx</span></span> |
| <span data-ttu-id="52f3f-134">Network</span><span class="sxs-lookup"><span data-stu-id="52f3f-134">Network</span></span> |<span data-ttu-id="52f3f-135">Bridged</span><span class="sxs-lookup"><span data-stu-id="52f3f-135">Bridged</span></span> |
| <span data-ttu-id="52f3f-136">Host Port</span><span class="sxs-lookup"><span data-stu-id="52f3f-136">Host Port</span></span> |<span data-ttu-id="52f3f-137">80</span><span class="sxs-lookup"><span data-stu-id="52f3f-137">80</span></span> |
| <span data-ttu-id="52f3f-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="52f3f-138">Protocol</span></span> |<span data-ttu-id="52f3f-139">TCP</span><span class="sxs-lookup"><span data-stu-id="52f3f-139">TCP</span></span> |

![New Application UI--General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos4.png)

![New Application UI--Docker Container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos5.png)

![New Application UI--Ports and Service Discovery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="52f3f-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span><span class="sxs-lookup"><span data-stu-id="52f3f-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="52f3f-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span><span class="sxs-lookup"><span data-stu-id="52f3f-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="52f3f-145">Then enter the following setting under the `portMappings` section of the application definition.</span><span class="sxs-lookup"><span data-stu-id="52f3f-145">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="52f3f-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span><span class="sxs-lookup"><span data-stu-id="52f3f-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="52f3f-147">You can switch this wizard out of JSON Mode after you make this change.</span><span class="sxs-lookup"><span data-stu-id="52f3f-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![New Application UI--port 80 example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="52f3f-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span><span class="sxs-lookup"><span data-stu-id="52f3f-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![New Application UI--health checks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="52f3f-151">The DC/OS cluster is deployed with set of private and public agents.</span><span class="sxs-lookup"><span data-stu-id="52f3f-151">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="52f3f-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span><span class="sxs-lookup"><span data-stu-id="52f3f-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="52f3f-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span><span class="sxs-lookup"><span data-stu-id="52f3f-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="52f3f-154">Then click **Create Application**.</span><span class="sxs-lookup"><span data-stu-id="52f3f-154">Then click **Create Application**.</span></span>

![New Application UI--public agent setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="52f3f-156">Back on the Marathon main page, you can see the deployment status for the container.</span><span class="sxs-lookup"><span data-stu-id="52f3f-156">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="52f3f-157">Initially you see a status of **Deploying**.</span><span class="sxs-lookup"><span data-stu-id="52f3f-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="52f3f-158">After a successful deployment, the status changes to **Running**.</span><span class="sxs-lookup"><span data-stu-id="52f3f-158">After a successful deployment, the status changes to **Running**.</span></span>

![Marathon main page UI--container deployment status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="52f3f-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="52f3f-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![DC/OS web UI--task running on the cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="52f3f-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span><span class="sxs-lookup"><span data-stu-id="52f3f-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![DC/OS web UI--task cluster node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="52f3f-164">Reach the container</span><span class="sxs-lookup"><span data-stu-id="52f3f-164">Reach the container</span></span>

<span data-ttu-id="52f3f-165">In this example, the application is running on a public agent node.</span><span class="sxs-lookup"><span data-stu-id="52f3f-165">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="52f3f-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span><span class="sxs-lookup"><span data-stu-id="52f3f-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="52f3f-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span><span class="sxs-lookup"><span data-stu-id="52f3f-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="52f3f-168">**REGION** is the region in which your resource group is located.</span><span class="sxs-lookup"><span data-stu-id="52f3f-168">**REGION** is the region in which your resource group is located.</span></span>

    ![Nginx from Internet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="52f3f-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="52f3f-170">Next steps</span></span>
* [<span data-ttu-id="52f3f-171">Work with DC/OS and the Marathon API</span><span class="sxs-lookup"><span data-stu-id="52f3f-171">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="52f3f-172">Deep dive on the Azure Container Service with Mesos</span><span class="sxs-lookup"><span data-stu-id="52f3f-172">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 












