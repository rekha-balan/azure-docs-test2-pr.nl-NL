---
title: Monitor an Azure Container Service cluster with Sysdig
description: Monitor an Azure Container Service cluster with Sysdig.
services: container-service
author: sauryadas
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 0c0f4fd1f3a8242061e198d7b5447656f9008e96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868575"
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="e9d59-103">Monitor an Azure Container Service cluster with Sysdig</span><span class="sxs-lookup"><span data-stu-id="e9d59-103">Monitor an Azure Container Service cluster with Sysdig</span></span>

<span data-ttu-id="e9d59-104">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="e9d59-104">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="e9d59-105">You need an account with Sysdig for this configuration.</span><span class="sxs-lookup"><span data-stu-id="e9d59-105">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e9d59-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9d59-106">Prerequisites</span></span>
<span data-ttu-id="e9d59-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="e9d59-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="e9d59-108">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="e9d59-108">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="e9d59-109">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span><span class="sxs-lookup"><span data-stu-id="e9d59-109">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="e9d59-110">Sysdig</span><span class="sxs-lookup"><span data-stu-id="e9d59-110">Sysdig</span></span>
<span data-ttu-id="e9d59-111">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span><span class="sxs-lookup"><span data-stu-id="e9d59-111">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span></span> <span data-ttu-id="e9d59-112">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span><span class="sxs-lookup"><span data-stu-id="e9d59-112">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="e9d59-113">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span><span class="sxs-lookup"><span data-stu-id="e9d59-113">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span></span> <span data-ttu-id="e9d59-114">This view is in the “Overview” section, which is currently in beta.</span><span class="sxs-lookup"><span data-stu-id="e9d59-114">This view is in the “Overview” section, which is currently in beta.</span></span> 

![Sysdig UI](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="e9d59-116">Configure a Sysdig deployment with Marathon</span><span class="sxs-lookup"><span data-stu-id="e9d59-116">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="e9d59-117">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span><span class="sxs-lookup"><span data-stu-id="e9d59-117">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="e9d59-118">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span><span class="sxs-lookup"><span data-stu-id="e9d59-118">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span></span>

![Sysdig in DC/OS Universe](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="e9d59-120">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span><span class="sxs-lookup"><span data-stu-id="e9d59-120">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="e9d59-121">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span><span class="sxs-lookup"><span data-stu-id="e9d59-121">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig API key](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="e9d59-123">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="e9d59-123">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span></span> 

![Sysdig configuration in the DC/OS Universe](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="e9d59-125">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span><span class="sxs-lookup"><span data-stu-id="e9d59-125">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span></span> <span data-ttu-id="e9d59-126">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span><span class="sxs-lookup"><span data-stu-id="e9d59-126">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span></span> 

![Sysdig configuration in the DC/OS Universe-instances](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="e9d59-128">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span><span class="sxs-lookup"><span data-stu-id="e9d59-128">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span></span> 

<span data-ttu-id="e9d59-129">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="e9d59-129">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
