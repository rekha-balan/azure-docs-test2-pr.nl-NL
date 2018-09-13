---
title: DC/OS agent pools for Azure Container Service
description: How the public and private agent pools work with an Azure Container Service DC/OS cluster
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 01/04/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 17029f51be9fed8fc36c5f919ece84acbf0461d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867208"
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="8bdc1-103">DC/OS agent pools for Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="8bdc1-103">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="8bdc1-104">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-104">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="8bdc1-105">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-105">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="8bdc1-106">The machines can be exposed to the internet (public) or kept internal (private).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-106">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="8bdc1-107">This article gives a brief overview of why there are public and private pools.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-107">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="8bdc1-108">**Private agents**: Private agent nodes run through a non-routable network.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-108">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="8bdc1-109">This network is only accessible from the admin zone or through the public zone edge router.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-109">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="8bdc1-110">By default, DC/OS launches apps on private agent nodes.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-110">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="8bdc1-111">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-111">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="8bdc1-112">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.8/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-112">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.8/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="8bdc1-113">Deploy agent pools</span><span class="sxs-lookup"><span data-stu-id="8bdc1-113">Deploy agent pools</span></span>

<span data-ttu-id="8bdc1-114">The DC/OS agent pools In Azure Container Service are created as follows:</span><span class="sxs-lookup"><span data-stu-id="8bdc1-114">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="8bdc1-115">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-115">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="8bdc1-116">The **public pool** initially contains a predetermined number of agent nodes.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-116">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="8bdc1-117">This pool is added automatically when the DC/OS cluster is provisioned.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-117">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="8bdc1-118">The private pool and the public pool are Azure virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-118">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="8bdc1-119">You can resize these pools after deployment.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-119">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="8bdc1-120">Use agent pools</span><span class="sxs-lookup"><span data-stu-id="8bdc1-120">Use agent pools</span></span>
<span data-ttu-id="8bdc1-121">By default, **Marathon** deploys any new application to the *private* agent nodes.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-121">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="8bdc1-122">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-122">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="8bdc1-123">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-123">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="8bdc1-124">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-124">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bdc1-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bdc1-125">Next steps</span></span>
* <span data-ttu-id="8bdc1-126">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="8bdc1-126">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="8bdc1-127">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span><span class="sxs-lookup"><span data-stu-id="8bdc1-127">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

