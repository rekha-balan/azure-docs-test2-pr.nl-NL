---
title: Monitor Azure DC/OS cluster - Operations Management
description: Monitor an Azure Container Service DC/OS cluster with Log Analytics.
services: container-service
author: keikhara
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: b326e5b686e14cefac4e6376bd3f26787ea1d10d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869792"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-log-analytics"></a><span data-ttu-id="81ed2-103">Monitor an Azure Container Service DC/OS cluster with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="81ed2-103">Monitor an Azure Container Service DC/OS cluster with Log Analytics</span></span>

<span data-ttu-id="81ed2-104">Log Analytics is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span><span class="sxs-lookup"><span data-stu-id="81ed2-104">Log Analytics is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="81ed2-105">Container Solution is a solution in Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span><span class="sxs-lookup"><span data-stu-id="81ed2-105">Container Solution is a solution in Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="81ed2-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span><span class="sxs-lookup"><span data-stu-id="81ed2-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="81ed2-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="81ed2-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-log-analytics-from-the-dcos-universe"></a><span data-ttu-id="81ed2-108">Setting up Log Analytics from the DC/OS universe</span><span class="sxs-lookup"><span data-stu-id="81ed2-108">Setting up Log Analytics from the DC/OS universe</span></span>


<span data-ttu-id="81ed2-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span><span class="sxs-lookup"><span data-stu-id="81ed2-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="81ed2-110">Pre-requisite</span><span class="sxs-lookup"><span data-stu-id="81ed2-110">Pre-requisite</span></span>
- <span data-ttu-id="81ed2-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span><span class="sxs-lookup"><span data-stu-id="81ed2-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="81ed2-112">Log Analytics Workspace Setup - see "Step 3" below</span><span class="sxs-lookup"><span data-stu-id="81ed2-112">Log Analytics Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="81ed2-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span><span class="sxs-lookup"><span data-stu-id="81ed2-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="81ed2-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span><span class="sxs-lookup"><span data-stu-id="81ed2-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="81ed2-115">Click **Install**.</span><span class="sxs-lookup"><span data-stu-id="81ed2-115">Click **Install**.</span></span> <span data-ttu-id="81ed2-116">You will see a pop up with the version information and an **Install Package** or **Advanced Installation** button.</span><span class="sxs-lookup"><span data-stu-id="81ed2-116">You will see a pop up with the version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="81ed2-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span><span class="sxs-lookup"><span data-stu-id="81ed2-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="81ed2-118">Here, you will be asked to enter the `wsid` (the Log Analytics workspace ID) and `wskey` (the primary key for the workspace id).</span><span class="sxs-lookup"><span data-stu-id="81ed2-118">Here, you will be asked to enter the `wsid` (the Log Analytics workspace ID) and `wskey` (the primary key for the workspace id).</span></span> <span data-ttu-id="81ed2-119">To get both `wsid` and `wskey` you need to create an account at <https://mms.microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="81ed2-119">To get both `wsid` and `wskey` you need to create an account at <https://mms.microsoft.com>.</span></span>
<span data-ttu-id="81ed2-120">Please follow the steps to create an account.</span><span class="sxs-lookup"><span data-stu-id="81ed2-120">Please follow the steps to create an account.</span></span> <span data-ttu-id="81ed2-121">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="81ed2-121">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="81ed2-122">Select the number of instances that you want and click the ‘Review and Install’ button.</span><span class="sxs-lookup"><span data-stu-id="81ed2-122">Select the number of instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="81ed2-123">Typically, you will want to have the number of instances equal to the number of VM’s you have in your agent cluster.</span><span class="sxs-lookup"><span data-stu-id="81ed2-123">Typically, you will want to have the number of instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="81ed2-124">OMS Agent for Linux installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span><span class="sxs-lookup"><span data-stu-id="81ed2-124">OMS Agent for Linux installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="81ed2-125">Setting up a simple OMS dashboard</span><span class="sxs-lookup"><span data-stu-id="81ed2-125">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="81ed2-126">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="81ed2-126">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="81ed2-127">There are two ways to do this: OMS Portal or Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81ed2-127">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="81ed2-128">OMS Portal</span><span class="sxs-lookup"><span data-stu-id="81ed2-128">OMS Portal</span></span> 

<span data-ttu-id="81ed2-129">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span><span class="sxs-lookup"><span data-stu-id="81ed2-129">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="81ed2-130">Once you are in the **Solution Gallery**, select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="81ed2-130">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="81ed2-131">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span><span class="sxs-lookup"><span data-stu-id="81ed2-131">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="81ed2-132">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span><span class="sxs-lookup"><span data-stu-id="81ed2-132">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="81ed2-133">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81ed2-133">Azure Portal</span></span> 

<span data-ttu-id="81ed2-134">Login to Azure portal at <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="81ed2-134">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="81ed2-135">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span><span class="sxs-lookup"><span data-stu-id="81ed2-135">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="81ed2-136">Then Type `containers` in search.</span><span class="sxs-lookup"><span data-stu-id="81ed2-136">Then Type `containers` in search.</span></span> <span data-ttu-id="81ed2-137">You will see "containers" in the search results.</span><span class="sxs-lookup"><span data-stu-id="81ed2-137">You will see "containers" in the search results.</span></span> <span data-ttu-id="81ed2-138">Select **Containers** and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="81ed2-138">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="81ed2-139">Once you click **Create**, it will ask you for your workspace.</span><span class="sxs-lookup"><span data-stu-id="81ed2-139">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="81ed2-140">Select your workspace or if you do not have one, create a new workspace.</span><span class="sxs-lookup"><span data-stu-id="81ed2-140">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="81ed2-141">Once you’ve selected your workspace, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="81ed2-141">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="81ed2-142">For more information about the Log Analytics Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="81ed2-142">For more information about the Log Analytics Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="81ed2-143">How to scale OMS Agent with ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="81ed2-143">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="81ed2-144">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span><span class="sxs-lookup"><span data-stu-id="81ed2-144">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="81ed2-145">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span><span class="sxs-lookup"><span data-stu-id="81ed2-145">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="81ed2-146">This will deploy to other nodes which have not yet deployed the OMS agent.</span><span class="sxs-lookup"><span data-stu-id="81ed2-146">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="81ed2-147">Uninstall MS OMS</span><span class="sxs-lookup"><span data-stu-id="81ed2-147">Uninstall MS OMS</span></span>

<span data-ttu-id="81ed2-148">To uninstall MS OMS enter the following command:</span><span class="sxs-lookup"><span data-stu-id="81ed2-148">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="81ed2-149">Let us know!!!</span><span class="sxs-lookup"><span data-stu-id="81ed2-149">Let us know!!!</span></span>
<span data-ttu-id="81ed2-150">What works?</span><span class="sxs-lookup"><span data-stu-id="81ed2-150">What works?</span></span> <span data-ttu-id="81ed2-151">What is missing?</span><span class="sxs-lookup"><span data-stu-id="81ed2-151">What is missing?</span></span> <span data-ttu-id="81ed2-152">What else do you need for this to be useful for you?</span><span class="sxs-lookup"><span data-stu-id="81ed2-152">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="81ed2-153">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="81ed2-153">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81ed2-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="81ed2-154">Next steps</span></span>

 <span data-ttu-id="81ed2-155">Now that you have set up Log Analytics to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="81ed2-155">Now that you have set up Log Analytics to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
