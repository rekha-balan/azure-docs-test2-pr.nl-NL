---
title: Manage Azure DC/OS cluster with Marathon UI
description: Deploy containers to an Azure Container Service cluster service by using the Marathon web UI.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 04/04/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a22bddf48f97d961d481e2aedb42f7d645f3e678
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865580"
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="feb38-103">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span><span class="sxs-lookup"><span data-stu-id="feb38-103">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>

<span data-ttu-id="feb38-104">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span><span class="sxs-lookup"><span data-stu-id="feb38-104">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="feb38-105">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span><span class="sxs-lookup"><span data-stu-id="feb38-105">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="feb38-106">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span><span class="sxs-lookup"><span data-stu-id="feb38-106">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="feb38-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="feb38-107">Prerequisites</span></span>
<span data-ttu-id="feb38-108">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="feb38-108">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="feb38-109">You also need to have remote connectivity to this cluster.</span><span class="sxs-lookup"><span data-stu-id="feb38-109">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="feb38-110">For more information on these items, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="feb38-110">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="feb38-111">Deploy an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="feb38-111">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="feb38-112">Connect to an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="feb38-112">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="feb38-113">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span><span class="sxs-lookup"><span data-stu-id="feb38-113">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="feb38-114">Explore the DC/OS UI</span><span class="sxs-lookup"><span data-stu-id="feb38-114">Explore the DC/OS UI</span></span>
<span data-ttu-id="feb38-115">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span><span class="sxs-lookup"><span data-stu-id="feb38-115">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="feb38-116">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span><span class="sxs-lookup"><span data-stu-id="feb38-116">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS UI](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="feb38-118">Explore the Marathon UI</span><span class="sxs-lookup"><span data-stu-id="feb38-118">Explore the Marathon UI</span></span>
<span data-ttu-id="feb38-119">To see the Marathon UI, browse to http://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="feb38-119">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="feb38-120">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="feb38-120">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="feb38-121">You can also see information about running containers and applications.</span><span class="sxs-lookup"><span data-stu-id="feb38-121">You can also see information about running containers and applications.</span></span>  

![Marathon UI](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="feb38-123">Deploy a Docker-formatted container</span><span class="sxs-lookup"><span data-stu-id="feb38-123">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="feb38-124">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span><span class="sxs-lookup"><span data-stu-id="feb38-124">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="feb38-125">Field</span><span class="sxs-lookup"><span data-stu-id="feb38-125">Field</span></span> | <span data-ttu-id="feb38-126">Value</span><span class="sxs-lookup"><span data-stu-id="feb38-126">Value</span></span> |
| --- | --- |
| <span data-ttu-id="feb38-127">ID</span><span class="sxs-lookup"><span data-stu-id="feb38-127">ID</span></span> |<span data-ttu-id="feb38-128">nginx</span><span class="sxs-lookup"><span data-stu-id="feb38-128">nginx</span></span> |
| <span data-ttu-id="feb38-129">Memory</span><span class="sxs-lookup"><span data-stu-id="feb38-129">Memory</span></span> | <span data-ttu-id="feb38-130">32</span><span class="sxs-lookup"><span data-stu-id="feb38-130">32</span></span> |
| <span data-ttu-id="feb38-131">Image</span><span class="sxs-lookup"><span data-stu-id="feb38-131">Image</span></span> |<span data-ttu-id="feb38-132">nginx</span><span class="sxs-lookup"><span data-stu-id="feb38-132">nginx</span></span> |
| <span data-ttu-id="feb38-133">Network</span><span class="sxs-lookup"><span data-stu-id="feb38-133">Network</span></span> |<span data-ttu-id="feb38-134">Bridged</span><span class="sxs-lookup"><span data-stu-id="feb38-134">Bridged</span></span> |
| <span data-ttu-id="feb38-135">Host Port</span><span class="sxs-lookup"><span data-stu-id="feb38-135">Host Port</span></span> |<span data-ttu-id="feb38-136">80</span><span class="sxs-lookup"><span data-stu-id="feb38-136">80</span></span> |
| <span data-ttu-id="feb38-137">Protocol</span><span class="sxs-lookup"><span data-stu-id="feb38-137">Protocol</span></span> |<span data-ttu-id="feb38-138">TCP</span><span class="sxs-lookup"><span data-stu-id="feb38-138">TCP</span></span> |

![New Application UI--General](./media/container-service-mesos-marathon-ui/dcos4.png)

![New Application UI--Docker Container](./media/container-service-mesos-marathon-ui/dcos5.png)

![New Application UI--Ports and Service Discovery](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="feb38-142">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span><span class="sxs-lookup"><span data-stu-id="feb38-142">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="feb38-143">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span><span class="sxs-lookup"><span data-stu-id="feb38-143">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="feb38-144">Then enter the following setting under the `portMappings` section of the application definition.</span><span class="sxs-lookup"><span data-stu-id="feb38-144">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="feb38-145">This example binds port 80 of the container to port 80 of the DC/OS agent.</span><span class="sxs-lookup"><span data-stu-id="feb38-145">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="feb38-146">You can switch this wizard out of JSON Mode after you make this change.</span><span class="sxs-lookup"><span data-stu-id="feb38-146">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![New Application UI--port 80 example](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="feb38-148">If you want to enable health checks, set a path on the **Health Checks** tab.</span><span class="sxs-lookup"><span data-stu-id="feb38-148">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![New Application UI--health checks](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="feb38-150">The DC/OS cluster is deployed with set of private and public agents.</span><span class="sxs-lookup"><span data-stu-id="feb38-150">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="feb38-151">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span><span class="sxs-lookup"><span data-stu-id="feb38-151">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="feb38-152">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span><span class="sxs-lookup"><span data-stu-id="feb38-152">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="feb38-153">Then click **Create Application**.</span><span class="sxs-lookup"><span data-stu-id="feb38-153">Then click **Create Application**.</span></span>

![New Application UI--public agent setting](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="feb38-155">Back on the Marathon main page, you can see the deployment status for the container.</span><span class="sxs-lookup"><span data-stu-id="feb38-155">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="feb38-156">Initially you see a status of **Deploying**.</span><span class="sxs-lookup"><span data-stu-id="feb38-156">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="feb38-157">After a successful deployment, the status changes to **Running**.</span><span class="sxs-lookup"><span data-stu-id="feb38-157">After a successful deployment, the status changes to **Running**.</span></span>

![Marathon main page UI--container deployment status](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="feb38-159">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="feb38-159">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![DC/OS web UI--task running on the cluster](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="feb38-161">To see the cluster node that the task is running on, click the **Nodes** tab.</span><span class="sxs-lookup"><span data-stu-id="feb38-161">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![DC/OS web UI--task cluster node](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="feb38-163">Reach the container</span><span class="sxs-lookup"><span data-stu-id="feb38-163">Reach the container</span></span>

<span data-ttu-id="feb38-164">In this example, the application is running on a public agent node.</span><span class="sxs-lookup"><span data-stu-id="feb38-164">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="feb38-165">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span><span class="sxs-lookup"><span data-stu-id="feb38-165">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="feb38-166">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span><span class="sxs-lookup"><span data-stu-id="feb38-166">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="feb38-167">**REGION** is the region in which your resource group is located.</span><span class="sxs-lookup"><span data-stu-id="feb38-167">**REGION** is the region in which your resource group is located.</span></span>

    ![Nginx from Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="feb38-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="feb38-169">Next steps</span></span>
* [<span data-ttu-id="feb38-170">Work with DC/OS and the Marathon API</span><span class="sxs-lookup"><span data-stu-id="feb38-170">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="feb38-171">Deep dive on the Azure Container Service with Mesos</span><span class="sxs-lookup"><span data-stu-id="feb38-171">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
