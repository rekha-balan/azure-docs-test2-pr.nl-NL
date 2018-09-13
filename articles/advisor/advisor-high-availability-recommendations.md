---
title: Azure Advisor High Availability recommendations | Microsoft Docs
description: Use Azure Advisor to improve high availability of your Azure deployments.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 502dd84e53ebc8b54b891902838726d525363050
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550681"
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="fbaa3-103">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="fbaa3-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="fbaa3-104">Azure Advisor helps you ensure and improve the continuity of your business-critical applications.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-104">Azure Advisor helps you ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="fbaa3-105">You can get high availability recommendations by Advisor from the **High Availability** tab of the Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-105">You can get high availability recommendations by Advisor from the **High Availability** tab of the Advisor dashboard.</span></span>

![High Availability button on the Advisor dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="fbaa3-107">Ensure virtual machine fault tolerance</span><span class="sxs-lookup"><span data-stu-id="fbaa3-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="fbaa3-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="fbaa3-109">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-109">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="fbaa3-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="fbaa3-111">You can choose either to create an availability set for the virtual machine or to add the virtual machine to an existing availability set.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-111">You can choose either to create an availability set for the virtual machine or to add the virtual machine to an existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="fbaa3-112">If you choose to create an availability set, you must add at least one more virtual machine into it.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-112">If you choose to create an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="fbaa3-113">We recommend that you group two or more virtual machines in an availability set to ensure that at least one machine is available during an outage.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-113">We recommend that you group two or more virtual machines in an availability set to ensure that at least one machine is available during an outage.</span></span>

![Advisor recommendation: For virtual machine redundancy, use availability sets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="fbaa3-115">Ensure availability set fault tolerance</span><span class="sxs-lookup"><span data-stu-id="fbaa3-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="fbaa3-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines to it.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines to it.</span></span> <span data-ttu-id="fbaa3-117">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-117">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="fbaa3-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="fbaa3-119">You can choose either to create a virtual machine or to use an existing virtual machine, and to add it to the availability set.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-119">You can choose either to create a virtual machine or to use an existing virtual machine, and to add it to the availability set.</span></span>  

![Advisor recommendation: Add one or more VMs to this availability set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="fbaa3-121">Ensure application gateway fault tolerance</span><span class="sxs-lookup"><span data-stu-id="fbaa3-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="fbaa3-122">To ensure the business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-122">To ensure the business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="fbaa3-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="fbaa3-124">It also identifies single- or multi-instance small application gateways and recommends migrating to medium or large SKUs.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-124">It also identifies single- or multi-instance small application gateways and recommends migrating to medium or large SKUs.</span></span> <span data-ttu-id="fbaa3-125">Advisor recommends these actions to ensure that your application gateway instances are configured to satisfy the current SLA requirements for these resources.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-125">Advisor recommends these actions to ensure that your application gateway instances are configured to satisfy the current SLA requirements for these resources.</span></span>

![Advisor recommendation: Deploy two or more medium or large sized application gateway instances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-the-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="fbaa3-127">Improve the performance and reliability of virtual machine disks</span><span class="sxs-lookup"><span data-stu-id="fbaa3-127">Improve the performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="fbaa3-128">Advisor identifies virtual machines with standard disks and recommends upgrading to premium disks.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-128">Advisor identifies virtual machines with standard disks and recommends upgrading to premium disks.</span></span>
 
<span data-ttu-id="fbaa3-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="fbaa3-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span><span class="sxs-lookup"><span data-stu-id="fbaa3-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="fbaa3-131">For the best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS to premium storage.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-131">For the best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS to premium storage.</span></span> 

<span data-ttu-id="fbaa3-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="fbaa3-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="fbaa3-134">You can choose to migrate your virtual machine disks to premium disks.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-134">You can choose to migrate your virtual machine disks to premium disks.</span></span> <span data-ttu-id="fbaa3-135">Premium disks are supported on most virtual machine SKUs.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="fbaa3-136">However, in some cases, if you want to use premium disks, you might need to upgrade your virtual machine SKUs as well.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-136">However, in some cases, if you want to use premium disks, you might need to upgrade your virtual machine SKUs as well.</span></span>

![Advisor recommendation: Improve the reliability of your virtual machine disks by upgrading to premium disks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="fbaa3-138">Protect your virtual machine data from accidental deletion</span><span class="sxs-lookup"><span data-stu-id="fbaa3-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="fbaa3-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="fbaa3-140">Setting up virtual machine backup ensures the availability of your business-critical data and offers protection against accidental deletion or corruption.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-140">Setting up virtual machine backup ensures the availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![Advisor recommendation: Configure virtual machine backup to protect your mission-critical data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="fbaa3-142">Access high availability recommendations in Advisor</span><span class="sxs-lookup"><span data-stu-id="fbaa3-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="fbaa3-143">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fbaa3-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fbaa3-144">In the left pane, click **More services**.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-144">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="fbaa3-145">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-145">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="fbaa3-146">The Advisor dashboard is displayed.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-146">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="fbaa3-147">On the Advisor dashboard, click the **High Availability** tab, and then select the subscription for which you want to receive recommendations.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-147">On the Advisor dashboard, click the **High Availability** tab, and then select the subscription for which you want to receive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="fbaa3-148">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-148">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="fbaa3-149">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-149">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="fbaa3-150">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-150">This is a *one-time operation*.</span></span> <span data-ttu-id="fbaa3-151">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="fbaa3-151">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbaa3-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbaa3-152">Next steps</span></span>

<span data-ttu-id="fbaa3-153">For more information about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="fbaa3-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="fbaa3-154">Introduction to Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="fbaa3-154">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="fbaa3-155">Get started with Advisor</span><span class="sxs-lookup"><span data-stu-id="fbaa3-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="fbaa3-156">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="fbaa3-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="fbaa3-157">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="fbaa3-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="fbaa3-158">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="fbaa3-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)







