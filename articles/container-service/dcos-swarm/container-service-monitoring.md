---
title: Monitor Azure DC/OS cluster - Datadog
description: Monitor an Azure Container Service cluster with Datadog. Use the DC/OS web UI to deploy the Datadog agents to your cluster.
services: container-service
author: sauryadas
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 029f36e4362704fcec240f6e88da5c96e903c317
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871159"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="d8b32-104">Monitor an Azure Container Service DC/OS cluster with Datadog</span><span class="sxs-lookup"><span data-stu-id="d8b32-104">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>

<span data-ttu-id="d8b32-105">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="d8b32-105">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="d8b32-106">You will need an account with Datadog for this configuration.</span><span class="sxs-lookup"><span data-stu-id="d8b32-106">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d8b32-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8b32-107">Prerequisites</span></span>
<span data-ttu-id="d8b32-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="d8b32-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="d8b32-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="d8b32-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="d8b32-110">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span><span class="sxs-lookup"><span data-stu-id="d8b32-110">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="d8b32-111">Datadog</span><span class="sxs-lookup"><span data-stu-id="d8b32-111">Datadog</span></span>
<span data-ttu-id="d8b32-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="d8b32-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="d8b32-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span><span class="sxs-lookup"><span data-stu-id="d8b32-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="d8b32-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span><span class="sxs-lookup"><span data-stu-id="d8b32-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="d8b32-115">Datadog splits metrics into containers and images.</span><span class="sxs-lookup"><span data-stu-id="d8b32-115">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="d8b32-116">An example of what the UI looks like for CPU usage is below.</span><span class="sxs-lookup"><span data-stu-id="d8b32-116">An example of what the UI looks like for CPU usage is below.</span></span>

![Datadog UI](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="d8b32-118">Configure a Datadog deployment with Marathon</span><span class="sxs-lookup"><span data-stu-id="d8b32-118">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="d8b32-119">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span><span class="sxs-lookup"><span data-stu-id="d8b32-119">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="d8b32-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="d8b32-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="d8b32-121">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span><span class="sxs-lookup"><span data-stu-id="d8b32-121">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog package within the DC/OS Universe](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="d8b32-123">Now to complete the configuration you will need a Datadog account or a free trial account.</span><span class="sxs-lookup"><span data-stu-id="d8b32-123">Now to complete the configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="d8b32-124">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="d8b32-124">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API key](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="d8b32-126">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="d8b32-126">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span></span> 

![Datadog configuration in the DC/OS Universe](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="d8b32-128">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span><span class="sxs-lookup"><span data-stu-id="d8b32-128">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span></span> <span data-ttu-id="d8b32-129">This is an interim solution.</span><span class="sxs-lookup"><span data-stu-id="d8b32-129">This is an interim solution.</span></span> <span data-ttu-id="d8b32-130">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="d8b32-130">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="d8b32-131">From there you will see Custom and Integration Dashboards.</span><span class="sxs-lookup"><span data-stu-id="d8b32-131">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="d8b32-132">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span><span class="sxs-lookup"><span data-stu-id="d8b32-132">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span></span> 

