---
title: Monitor Azure DC/OS cluster - Dynatrace
description: Monitor an Azure Container Service DC/OS cluster with Dynatrace. Deploy the Dynatrace OneAgent by using the DC/OS dashboard.
services: container-service
author: MartinGoodwell
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 3d1bfc3bb61781d487c40831edd5da6fcb5a7df9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857954"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="27700-104">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="27700-104">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>

<span data-ttu-id="27700-105">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="27700-105">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="27700-106">You need an account with Dynatrace SaaS/Managed for this configuration.</span><span class="sxs-lookup"><span data-stu-id="27700-106">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="27700-107">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="27700-107">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="27700-108">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span><span class="sxs-lookup"><span data-stu-id="27700-108">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="27700-109">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span><span class="sxs-lookup"><span data-stu-id="27700-109">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="27700-110">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span><span class="sxs-lookup"><span data-stu-id="27700-110">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="27700-111">The following figure shows the Dynatrace UI:</span><span class="sxs-lookup"><span data-stu-id="27700-111">The following figure shows the Dynatrace UI:</span></span>

![Dynatrace UI](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="27700-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="27700-113">Prerequisites</span></span> 
<span data-ttu-id="27700-114">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="27700-114">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="27700-115">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="27700-115">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="27700-116">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span><span class="sxs-lookup"><span data-stu-id="27700-116">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="27700-117">Configure a Dynatrace deployment with Marathon</span><span class="sxs-lookup"><span data-stu-id="27700-117">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="27700-118">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span><span class="sxs-lookup"><span data-stu-id="27700-118">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="27700-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="27700-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="27700-120">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="27700-120">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace in DC/OS Universe](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="27700-122">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span><span class="sxs-lookup"><span data-stu-id="27700-122">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="27700-123">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="27700-123">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace Set up PaaS integration](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="27700-125">On the page, select **Set up PaaS integration**.</span><span class="sxs-lookup"><span data-stu-id="27700-125">On the page, select **Set up PaaS integration**.</span></span> 

    ![Dynatrace API token](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="27700-127">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="27700-127">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![Dynatrace OneAgent configuration in the DC/OS Universe](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="27700-129">Set the instances to the number of nodes you intend to run.</span><span class="sxs-lookup"><span data-stu-id="27700-129">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="27700-130">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span><span class="sxs-lookup"><span data-stu-id="27700-130">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="27700-131">If you prefer, you can also set this to a value like 1000000.</span><span class="sxs-lookup"><span data-stu-id="27700-131">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="27700-132">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span><span class="sxs-lookup"><span data-stu-id="27700-132">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![Dynatrace configuration in the DC/OS Universe-instances](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="27700-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="27700-134">Next steps</span></span>

<span data-ttu-id="27700-135">Once you've installed the package, navigate back to the Dynatrace dashboard.</span><span class="sxs-lookup"><span data-stu-id="27700-135">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="27700-136">You can explore the different usage metrics for the containers within your cluster.</span><span class="sxs-lookup"><span data-stu-id="27700-136">You can explore the different usage metrics for the containers within your cluster.</span></span> 