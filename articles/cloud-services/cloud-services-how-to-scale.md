---
title: Auto scale a cloud service in the classic portal | Microsoft Docs
description: (classic) Learn how to use the classic portal to configure auto scale rules for a cloud service web role or worker role in Azure.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: adegeo
ms.openlocfilehash: 2b8836424483d1bccd238feec68537463e065b9b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563020"
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="edce7-103">How to configure auto scaling for a Cloud Service in the classic portal</span><span class="sxs-lookup"><span data-stu-id="edce7-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-scale-portal.md)
> * [Azure classic portal](cloud-services-how-to-scale.md)

<span data-ttu-id="edce7-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span><span class="sxs-lookup"><span data-stu-id="edce7-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="edce7-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span><span class="sxs-lookup"><span data-stu-id="edce7-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> This article focuses on Cloud Service web and worker roles. When you create a virtual machine (classic) directly, it is hosted in a cloud service. Some of this information applies to these types of virtual machines. Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure. For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="edce7-113">You should consider the following information before you configure scaling for your application:</span><span class="sxs-lookup"><span data-stu-id="edce7-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="edce7-114">Scaling is affected by core usage.</span><span class="sxs-lookup"><span data-stu-id="edce7-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="edce7-115">Larger role instances use more cores.</span><span class="sxs-lookup"><span data-stu-id="edce7-115">Larger role instances use more cores.</span></span> <span data-ttu-id="edce7-116">You can scale an application only within the limit of cores for your subscription.</span><span class="sxs-lookup"><span data-stu-id="edce7-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="edce7-117">For example, say your subscription has a limit of 20 cores.</span><span class="sxs-lookup"><span data-stu-id="edce7-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="edce7-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span><span class="sxs-lookup"><span data-stu-id="edce7-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="edce7-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="edce7-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="edce7-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span><span class="sxs-lookup"><span data-stu-id="edce7-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="edce7-121">For more information, see [How to use the Queue Storage Service](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="edce7-121">For more information, see [How to use the Queue Storage Service](../storage/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="edce7-122">You can scale resources that are linked to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="edce7-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="edce7-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="edce7-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="edce7-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span><span class="sxs-lookup"><span data-stu-id="edce7-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="edce7-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="edce7-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

> [!WARNING]
> Automatic scaling only works with Classic Azure Storage Accounts. It does not work with Azure Resource Manager Storage Accounts.

## <a name="schedule-scaling"></a><span data-ttu-id="edce7-128">Schedule scaling</span><span class="sxs-lookup"><span data-stu-id="edce7-128">Schedule scaling</span></span>
<span data-ttu-id="edce7-129">By default, all roles do not follow a specific schedule.</span><span class="sxs-lookup"><span data-stu-id="edce7-129">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="edce7-130">Therefore, any settings changed apply to all times and all days throughout the year.</span><span class="sxs-lookup"><span data-stu-id="edce7-130">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="edce7-131">If you want, you can setup manual or automatic scaling for one of the following modes:</span><span class="sxs-lookup"><span data-stu-id="edce7-131">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="edce7-132">Weekdays</span><span class="sxs-lookup"><span data-stu-id="edce7-132">Weekdays</span></span>
* <span data-ttu-id="edce7-133">Weekends</span><span class="sxs-lookup"><span data-stu-id="edce7-133">Weekends</span></span>
* <span data-ttu-id="edce7-134">Week nights</span><span class="sxs-lookup"><span data-stu-id="edce7-134">Week nights</span></span>
* <span data-ttu-id="edce7-135">Week mornings</span><span class="sxs-lookup"><span data-stu-id="edce7-135">Week mornings</span></span>
* <span data-ttu-id="edce7-136">Specific dates</span><span class="sxs-lookup"><span data-stu-id="edce7-136">Specific dates</span></span>
* <span data-ttu-id="edce7-137">Specific date ranges</span><span class="sxs-lookup"><span data-stu-id="edce7-137">Specific date ranges</span></span>

<span data-ttu-id="edce7-138">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span><span class="sxs-lookup"><span data-stu-id="edce7-138">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="edce7-139">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span><span class="sxs-lookup"><span data-stu-id="edce7-139">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="edce7-140">Click the **set up schedule times** button for each role you want to change.</span><span class="sxs-lookup"><span data-stu-id="edce7-140">Click the **set up schedule times** button for each role you want to change.</span></span>

![Cloud service automatic scaling based on a schedule][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="edce7-142">Manual scale</span><span class="sxs-lookup"><span data-stu-id="edce7-142">Manual scale</span></span>
<span data-ttu-id="edce7-143">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span><span class="sxs-lookup"><span data-stu-id="edce7-143">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="edce7-144">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span><span class="sxs-lookup"><span data-stu-id="edce7-144">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="edce7-145">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="edce7-145">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.

2. <span data-ttu-id="edce7-147">Click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="edce7-147">Click **Scale**.</span></span>
3. <span data-ttu-id="edce7-148">Select the schedule you want to change scaling options for.</span><span class="sxs-lookup"><span data-stu-id="edce7-148">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="edce7-149">*No scheduled times* is the default if you have no schedules defined.</span><span class="sxs-lookup"><span data-stu-id="edce7-149">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="edce7-150">Find the **Scale by metric** section and select **NONE**.</span><span class="sxs-lookup"><span data-stu-id="edce7-150">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="edce7-151">This setting is the default for all roles.</span><span class="sxs-lookup"><span data-stu-id="edce7-151">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="edce7-152">Each role in the cloud service has a slider for changing the number of instances to use.</span><span class="sxs-lookup"><span data-stu-id="edce7-152">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Manually scale a cloud service role][manual_scale]
   
    <span data-ttu-id="edce7-154">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="edce7-154">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="edce7-155">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="edce7-155">Click **Save**.</span></span>  
   <span data-ttu-id="edce7-156">Role instances are added or removed based on your selections.</span><span class="sxs-lookup"><span data-stu-id="edce7-156">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.

## <a name="automatic-scale---cpu"></a><span data-ttu-id="edce7-158">Automatic scale - CPU</span><span class="sxs-lookup"><span data-stu-id="edce7-158">Automatic scale - CPU</span></span>
<span data-ttu-id="edce7-159">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span><span class="sxs-lookup"><span data-stu-id="edce7-159">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="edce7-160">Role instances are created or deleted when this happens.</span><span class="sxs-lookup"><span data-stu-id="edce7-160">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="edce7-161">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="edce7-161">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.

2. <span data-ttu-id="edce7-163">Click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="edce7-163">Click **Scale**.</span></span>
3. <span data-ttu-id="edce7-164">Select the schedule you want to change scaling options for.</span><span class="sxs-lookup"><span data-stu-id="edce7-164">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="edce7-165">*No scheduled times* is the default if you have no schedules defined.</span><span class="sxs-lookup"><span data-stu-id="edce7-165">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="edce7-166">Find the **Scale by metric** section and select **CPU**.</span><span class="sxs-lookup"><span data-stu-id="edce7-166">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="edce7-167">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span><span class="sxs-lookup"><span data-stu-id="edce7-167">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Scale a cloud service role by cpu load][cpu_scale]

> [!TIP]
> Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.

## <a name="automatic-scale---queue"></a><span data-ttu-id="edce7-170">Automatic scale - Queue</span><span class="sxs-lookup"><span data-stu-id="edce7-170">Automatic scale - Queue</span></span>
<span data-ttu-id="edce7-171">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span><span class="sxs-lookup"><span data-stu-id="edce7-171">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="edce7-172">Role instances are created or deleted when this happens.</span><span class="sxs-lookup"><span data-stu-id="edce7-172">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="edce7-173">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="edce7-173">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.

2. <span data-ttu-id="edce7-175">Click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="edce7-175">Click **Scale**.</span></span>
3. <span data-ttu-id="edce7-176">Find the **Scale by metric** section and select **QUEUE**.</span><span class="sxs-lookup"><span data-stu-id="edce7-176">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="edce7-177">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span><span class="sxs-lookup"><span data-stu-id="edce7-177">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Scale a cloud service role by a message queue][queue_scale]

> [!TIP]
> Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.

## <a name="scale-linked-resources"></a><span data-ttu-id="edce7-180">Scale linked resources</span><span class="sxs-lookup"><span data-stu-id="edce7-180">Scale linked resources</span></span>
<span data-ttu-id="edce7-181">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span><span class="sxs-lookup"><span data-stu-id="edce7-181">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="edce7-182">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span><span class="sxs-lookup"><span data-stu-id="edce7-182">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="edce7-183">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="edce7-183">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.

2. <span data-ttu-id="edce7-185">Click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="edce7-185">Click **Scale**.</span></span>
3. <span data-ttu-id="edce7-186">Find the **linked resources** section and click **Manage scale for this database**.</span><span class="sxs-lookup"><span data-stu-id="edce7-186">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > If you don't see a **linked resources** section, you probably do not have any linked resources.

![][linked_resource]

[manual_scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/tip.png
[scale_schedules]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/schedules.png
[scale_popup]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-scale/linked-resources.png







