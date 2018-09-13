---
title: Auto scale a cloud service in the portal (classic portal) | Microsoft Docs
description: Learn how to use the portal to configure auto scale rules for a cloud service web role or worker role in Azure.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: adegeo
ms.openlocfilehash: 351ef4e18793777ae17fe1d22df45e85a5fb3833
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563157"
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="028f8-103">How to configure auto scaling for a Cloud Service in the portal</span><span class="sxs-lookup"><span data-stu-id="028f8-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-scale-portal.md)
> * [Azure classic portal](cloud-services-how-to-scale.md)

<span data-ttu-id="028f8-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span><span class="sxs-lookup"><span data-stu-id="028f8-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="028f8-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span><span class="sxs-lookup"><span data-stu-id="028f8-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="028f8-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="028f8-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> This article focuses on Cloud Service web and worker roles. When you create a virtual machine (classic) directly, it is hosted in a cloud service. You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.

## <a name="considerations"></a><span data-ttu-id="028f8-112">Considerations</span><span class="sxs-lookup"><span data-stu-id="028f8-112">Considerations</span></span>
<span data-ttu-id="028f8-113">You should consider the following information before you configure scaling for your application:</span><span class="sxs-lookup"><span data-stu-id="028f8-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="028f8-114">Scaling is affected by core usage.</span><span class="sxs-lookup"><span data-stu-id="028f8-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="028f8-115">Larger role instances use more cores.</span><span class="sxs-lookup"><span data-stu-id="028f8-115">Larger role instances use more cores.</span></span> <span data-ttu-id="028f8-116">You can scale an application only within the limit of cores for your subscription.</span><span class="sxs-lookup"><span data-stu-id="028f8-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="028f8-117">For example, say your subscription has a limit of 20 cores.</span><span class="sxs-lookup"><span data-stu-id="028f8-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="028f8-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span><span class="sxs-lookup"><span data-stu-id="028f8-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="028f8-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="028f8-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="028f8-120">You can scale based on a queue message threshold.</span><span class="sxs-lookup"><span data-stu-id="028f8-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="028f8-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="028f8-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="028f8-122">You can also scale other resources associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="028f8-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="028f8-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span><span class="sxs-lookup"><span data-stu-id="028f8-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="028f8-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="028f8-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

> [!WARNING]
> Automatic scaling only works with Classic Azure Storage Accounts. It does not work with Azure Resource Manager Storage Accounts.


## <a name="where-scale-is-located"></a><span data-ttu-id="028f8-127">Where scale is located</span><span class="sxs-lookup"><span data-stu-id="028f8-127">Where scale is located</span></span>
<span data-ttu-id="028f8-128">After you select your cloud service, you should have the cloud service blade visible.</span><span class="sxs-lookup"><span data-stu-id="028f8-128">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="028f8-129">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="028f8-129">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="028f8-130">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span><span class="sxs-lookup"><span data-stu-id="028f8-130">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="028f8-131">Select the **scale** tile.</span><span class="sxs-lookup"><span data-stu-id="028f8-131">Select the **scale** tile.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="028f8-132">Automatic scale</span><span class="sxs-lookup"><span data-stu-id="028f8-132">Automatic scale</span></span>
<span data-ttu-id="028f8-133">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span><span class="sxs-lookup"><span data-stu-id="028f8-133">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="028f8-134">Manual is as you would expect, you set the absolute count of instances.</span><span class="sxs-lookup"><span data-stu-id="028f8-134">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="028f8-135">Automatic however allows you to set rules that govern how and by how much you should scale.</span><span class="sxs-lookup"><span data-stu-id="028f8-135">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="028f8-136">Set the **Scale by** option to **schedule and performance rules**.</span><span class="sxs-lookup"><span data-stu-id="028f8-136">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![Cloud services scale settings with profile and rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="028f8-138">An existing profile.</span><span class="sxs-lookup"><span data-stu-id="028f8-138">An existing profile.</span></span>
2. <span data-ttu-id="028f8-139">Add a rule for the parent profile.</span><span class="sxs-lookup"><span data-stu-id="028f8-139">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="028f8-140">Add another profile.</span><span class="sxs-lookup"><span data-stu-id="028f8-140">Add another profile.</span></span>

<span data-ttu-id="028f8-141">Select **Add Profile**.</span><span class="sxs-lookup"><span data-stu-id="028f8-141">Select **Add Profile**.</span></span> <span data-ttu-id="028f8-142">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span><span class="sxs-lookup"><span data-stu-id="028f8-142">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="028f8-143">After you have configured the profile and rules, select the **Save** icon at the top.</span><span class="sxs-lookup"><span data-stu-id="028f8-143">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="028f8-144">Profile</span><span class="sxs-lookup"><span data-stu-id="028f8-144">Profile</span></span>
<span data-ttu-id="028f8-145">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span><span class="sxs-lookup"><span data-stu-id="028f8-145">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="028f8-146">**Always**</span><span class="sxs-lookup"><span data-stu-id="028f8-146">**Always**</span></span>
  
    <span data-ttu-id="028f8-147">Always keep this range of instances available.</span><span class="sxs-lookup"><span data-stu-id="028f8-147">Always keep this range of instances available.</span></span>  
  
    ![Cloud service that always scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="028f8-149">**Recurrence**</span><span class="sxs-lookup"><span data-stu-id="028f8-149">**Recurrence**</span></span>
  
    <span data-ttu-id="028f8-150">Choose a set of days of the week to scale.</span><span class="sxs-lookup"><span data-stu-id="028f8-150">Choose a set of days of the week to scale.</span></span>
  
    ![Cloud service scale with a recurrence schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="028f8-152">**Fixed Date**</span><span class="sxs-lookup"><span data-stu-id="028f8-152">**Fixed Date**</span></span>
  
    <span data-ttu-id="028f8-153">A fixed date range to scale the role.</span><span class="sxs-lookup"><span data-stu-id="028f8-153">A fixed date range to scale the role.</span></span>
  
    ![CLoud service scale with a fixed date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="028f8-155">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span><span class="sxs-lookup"><span data-stu-id="028f8-155">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="028f8-156">Rule</span><span class="sxs-lookup"><span data-stu-id="028f8-156">Rule</span></span>
<span data-ttu-id="028f8-157">Rules are added to a profile and represent a condition that triggers the scale.</span><span class="sxs-lookup"><span data-stu-id="028f8-157">Rules are added to a profile and represent a condition that triggers the scale.</span></span> 

<span data-ttu-id="028f8-158">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span><span class="sxs-lookup"><span data-stu-id="028f8-158">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="028f8-159">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="028f8-159">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="028f8-160">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span><span class="sxs-lookup"><span data-stu-id="028f8-160">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="028f8-161">Back to manual scale</span><span class="sxs-lookup"><span data-stu-id="028f8-161">Back to manual scale</span></span>
<span data-ttu-id="028f8-162">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span><span class="sxs-lookup"><span data-stu-id="028f8-162">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![Cloud services scale settings with profile and rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="028f8-164">This setting removes automated scaling from the role and then you can set the instance count directly.</span><span class="sxs-lookup"><span data-stu-id="028f8-164">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span> 

1. <span data-ttu-id="028f8-165">The scale (manual or automated) option.</span><span class="sxs-lookup"><span data-stu-id="028f8-165">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="028f8-166">A role instance slider to set the instances to scale to.</span><span class="sxs-lookup"><span data-stu-id="028f8-166">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="028f8-167">Instances of the role to scale to.</span><span class="sxs-lookup"><span data-stu-id="028f8-167">Instances of the role to scale to.</span></span>

<span data-ttu-id="028f8-168">After you have configured the scale settings, select the **Save** icon at the top.</span><span class="sxs-lookup"><span data-stu-id="028f8-168">After you have configured the scale settings, select the **Save** icon at the top.</span></span>









