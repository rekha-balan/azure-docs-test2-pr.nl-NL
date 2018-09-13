---
title: DC/OS agent pools for Azure Container Service | Microsoft Docs
description: How the public and private agent pools work with an Azure Container Service DC/OS cluster
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: 36d657c9-8845-4bf7-bed2-088323b67406
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.openlocfilehash: cffc65e25ae8eab90a9879a0030b78b3b77890b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552098"
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="e6a87-104">DC/OS agent pools for Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e6a87-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="e6a87-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span><span class="sxs-lookup"><span data-stu-id="e6a87-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="e6a87-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span><span class="sxs-lookup"><span data-stu-id="e6a87-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="e6a87-107">The machines can be exposed to the internet (public) or kept internal (private).</span><span class="sxs-lookup"><span data-stu-id="e6a87-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="e6a87-108">This article gives a brief overview of why there are public and private pools.</span><span class="sxs-lookup"><span data-stu-id="e6a87-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="e6a87-109">**Private agents**: Private agent nodes run through a non-routable network.</span><span class="sxs-lookup"><span data-stu-id="e6a87-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="e6a87-110">This network is only accessible from the admin zone or through the public zone edge router.</span><span class="sxs-lookup"><span data-stu-id="e6a87-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="e6a87-111">By default, DC/OS launches apps on private agent nodes.</span><span class="sxs-lookup"><span data-stu-id="e6a87-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="e6a87-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span><span class="sxs-lookup"><span data-stu-id="e6a87-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="e6a87-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e6a87-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="e6a87-114">Deploy agent pools</span><span class="sxs-lookup"><span data-stu-id="e6a87-114">Deploy agent pools</span></span>

<span data-ttu-id="e6a87-115">The DC/OS agent pools In Azure Container Service are created as follows:</span><span class="sxs-lookup"><span data-stu-id="e6a87-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="e6a87-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e6a87-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="e6a87-117">The **public pool** initially contains a predetermined number of agent nodes.</span><span class="sxs-lookup"><span data-stu-id="e6a87-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="e6a87-118">This pool is added automatically when the DC/OS cluster is provisioned.</span><span class="sxs-lookup"><span data-stu-id="e6a87-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="e6a87-119">The private pool and the public pool are Azure virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="e6a87-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="e6a87-120">You can resize these pools after deployment.</span><span class="sxs-lookup"><span data-stu-id="e6a87-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="e6a87-121">Use agent pools</span><span class="sxs-lookup"><span data-stu-id="e6a87-121">Use agent pools</span></span>
<span data-ttu-id="e6a87-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span><span class="sxs-lookup"><span data-stu-id="e6a87-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="e6a87-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span><span class="sxs-lookup"><span data-stu-id="e6a87-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="e6a87-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span><span class="sxs-lookup"><span data-stu-id="e6a87-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="e6a87-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span><span class="sxs-lookup"><span data-stu-id="e6a87-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6a87-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6a87-126">Next steps</span></span>
* <span data-ttu-id="e6a87-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="e6a87-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="e6a87-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span><span class="sxs-lookup"><span data-stu-id="e6a87-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

