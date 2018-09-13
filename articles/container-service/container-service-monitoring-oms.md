---
title: Monitor Azure DC/OS cluster - Operations Management | Microsoft Docs
description: Monitor an Azure Container Service DC/OS cluster with Microsoft Operations Management Suite.
services: container-service
documentationcenter: ''
author: keikhara
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: ''
ms.assetid: 01f1a77e-f3e1-4ec0-ad4c-d91298afa55c
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.openlocfilehash: 4be918cc291be70a34591c8b0a074d7e11589dc5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669354"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="e578c-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="e578c-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="e578c-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e578c-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="e578c-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span><span class="sxs-lookup"><span data-stu-id="e578c-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="e578c-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span><span class="sxs-lookup"><span data-stu-id="e578c-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="e578c-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="e578c-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-the-dcos-universe"></a><span data-ttu-id="e578c-108">Setting up OMS from the DC/OS universe</span><span class="sxs-lookup"><span data-stu-id="e578c-108">Setting up OMS from the DC/OS universe</span></span>


<span data-ttu-id="e578c-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span><span class="sxs-lookup"><span data-stu-id="e578c-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="e578c-110">Pre-requisite</span><span class="sxs-lookup"><span data-stu-id="e578c-110">Pre-requisite</span></span>
- <span data-ttu-id="e578c-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span><span class="sxs-lookup"><span data-stu-id="e578c-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="e578c-112">Microsoft OMS Workspace Setup - see "Step 3" below</span><span class="sxs-lookup"><span data-stu-id="e578c-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="e578c-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span><span class="sxs-lookup"><span data-stu-id="e578c-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="e578c-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span><span class="sxs-lookup"><span data-stu-id="e578c-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="e578c-115">Click **Install**.</span><span class="sxs-lookup"><span data-stu-id="e578c-115">Click **Install**.</span></span> <span data-ttu-id="e578c-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span><span class="sxs-lookup"><span data-stu-id="e578c-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="e578c-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span><span class="sxs-lookup"><span data-stu-id="e578c-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image3.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="e578c-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span><span class="sxs-lookup"><span data-stu-id="e578c-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span></span> <span data-ttu-id="e578c-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="e578c-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>.</span></span>
<span data-ttu-id="e578c-120">Please follow the steps to create an account.</span><span class="sxs-lookup"><span data-stu-id="e578c-120">Please follow the steps to create an account.</span></span> <span data-ttu-id="e578c-121">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="e578c-121">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="e578c-122">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span><span class="sxs-lookup"><span data-stu-id="e578c-122">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="e578c-123">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span><span class="sxs-lookup"><span data-stu-id="e578c-123">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="e578c-124">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span><span class="sxs-lookup"><span data-stu-id="e578c-124">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="e578c-125">Setting up a simple OMS dashboard</span><span class="sxs-lookup"><span data-stu-id="e578c-125">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="e578c-126">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="e578c-126">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="e578c-127">There are two ways to do this: OMS Portal or Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e578c-127">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="e578c-128">OMS Portal</span><span class="sxs-lookup"><span data-stu-id="e578c-128">OMS Portal</span></span> 

<span data-ttu-id="e578c-129">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span><span class="sxs-lookup"><span data-stu-id="e578c-129">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="e578c-130">Once you are in the **Solution Gallery**, select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="e578c-130">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="e578c-131">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span><span class="sxs-lookup"><span data-stu-id="e578c-131">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="e578c-132">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span><span class="sxs-lookup"><span data-stu-id="e578c-132">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="e578c-133">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e578c-133">Azure Portal</span></span> 

<span data-ttu-id="e578c-134">Login to Azure portal at <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="e578c-134">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="e578c-135">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span><span class="sxs-lookup"><span data-stu-id="e578c-135">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="e578c-136">Then Type `containers` in search.</span><span class="sxs-lookup"><span data-stu-id="e578c-136">Then Type `containers` in search.</span></span> <span data-ttu-id="e578c-137">You will see "containers" in the search results.</span><span class="sxs-lookup"><span data-stu-id="e578c-137">You will see "containers" in the search results.</span></span> <span data-ttu-id="e578c-138">Select **Containers** and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e578c-138">Select **Containers** and click **Create**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="e578c-139">Once you click **Create**, it will ask you for your workspace.</span><span class="sxs-lookup"><span data-stu-id="e578c-139">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="e578c-140">Select your workspace or if you do not have one, create a new workspace.</span><span class="sxs-lookup"><span data-stu-id="e578c-140">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="e578c-141">Once you’ve selected your workspace, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e578c-141">Once you’ve selected your workspace, click **Create**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="e578c-142">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="e578c-142">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="e578c-143">How to scale OMS Agent with ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="e578c-143">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="e578c-144">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span><span class="sxs-lookup"><span data-stu-id="e578c-144">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="e578c-145">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span><span class="sxs-lookup"><span data-stu-id="e578c-145">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="e578c-146">This will deploy to other nodes which have not yet deployed the OMS agent.</span><span class="sxs-lookup"><span data-stu-id="e578c-146">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="e578c-147">Uninstall MS OMS</span><span class="sxs-lookup"><span data-stu-id="e578c-147">Uninstall MS OMS</span></span>

<span data-ttu-id="e578c-148">To uninstall MS OMS enter the following command:</span><span class="sxs-lookup"><span data-stu-id="e578c-148">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="e578c-149">Let us know!!!</span><span class="sxs-lookup"><span data-stu-id="e578c-149">Let us know!!!</span></span>
<span data-ttu-id="e578c-150">What works?</span><span class="sxs-lookup"><span data-stu-id="e578c-150">What works?</span></span> <span data-ttu-id="e578c-151">What is missing?</span><span class="sxs-lookup"><span data-stu-id="e578c-151">What is missing?</span></span> <span data-ttu-id="e578c-152">What else do you need for this to be useful for you?</span><span class="sxs-lookup"><span data-stu-id="e578c-152">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="e578c-153">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="e578c-153">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e578c-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="e578c-154">Next steps</span></span>

 <span data-ttu-id="e578c-155">Now that you have set up OMS to monitor your containers,[see your container dashboard](../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="e578c-155">Now that you have set up OMS to monitor your containers,[see your container dashboard](../log-analytics/log-analytics-containers.md).</span></span>












