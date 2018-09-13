---
title: Get started with Azure Scheduler in Azure portal | Microsoft Docs
description: Get started with Azure Scheduler in Azure portal
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: ''
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 229c11733839a5ef88ed187ed7c43f7975b44c73
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662726"
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="48519-103">Get started with Azure Scheduler in Azure portal</span><span class="sxs-lookup"><span data-stu-id="48519-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="48519-104">It's easy to create scheduled jobs in Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="48519-104">It's easy to create scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="48519-105">In this tutorial, you'll learn how to create a job.</span><span class="sxs-lookup"><span data-stu-id="48519-105">In this tutorial, you'll learn how to create a job.</span></span> <span data-ttu-id="48519-106">You'll also learn Scheduler's monitoring and management capabilities.</span><span class="sxs-lookup"><span data-stu-id="48519-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="48519-107">Create a job</span><span class="sxs-lookup"><span data-stu-id="48519-107">Create a job</span></span>
1. <span data-ttu-id="48519-108">Sign in to [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="48519-108">Sign in to [Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="48519-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48519-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="48519-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span><span class="sxs-lookup"><span data-stu-id="48519-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="48519-111">In the **Scheduler Job** screen, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="48519-111">In the **Scheduler Job** screen, enter the following information:</span></span>
   
   1. <span data-ttu-id="48519-112">**Name:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="48519-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="48519-113">**Subscription:** Your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="48519-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="48519-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span><span class="sxs-lookup"><span data-stu-id="48519-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="48519-115">Next, in **Action Settings**, define the following values:</span><span class="sxs-lookup"><span data-stu-id="48519-115">Next, in **Action Settings**, define the following values:</span></span>
   
   1. <span data-ttu-id="48519-116">**Action Type:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="48519-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="48519-117">**Method:** `GET`</span><span class="sxs-lookup"><span data-stu-id="48519-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="48519-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="48519-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="48519-119">Finally, let's define a schedule.</span><span class="sxs-lookup"><span data-stu-id="48519-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="48519-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span><span class="sxs-lookup"><span data-stu-id="48519-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="48519-121">**Recurrence**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="48519-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="48519-122">**Start**: Today's date</span><span class="sxs-lookup"><span data-stu-id="48519-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="48519-123">**Recur every**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="48519-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="48519-124">**End by**: Two days from today's date</span><span class="sxs-lookup"><span data-stu-id="48519-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="48519-125">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="48519-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="48519-126">Manage and monitor jobs</span><span class="sxs-lookup"><span data-stu-id="48519-126">Manage and monitor jobs</span></span>
<span data-ttu-id="48519-127">Once a job is created, it appears in the main Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="48519-127">Once a job is created, it appears in the main Azure dashboard.</span></span> <span data-ttu-id="48519-128">Click the job and a new window opens with the following tabs:</span><span class="sxs-lookup"><span data-stu-id="48519-128">Click the job and a new window opens with the following tabs:</span></span>

1. <span data-ttu-id="48519-129">Properties</span><span class="sxs-lookup"><span data-stu-id="48519-129">Properties</span></span>  
2. <span data-ttu-id="48519-130">Action Settings</span><span class="sxs-lookup"><span data-stu-id="48519-130">Action Settings</span></span>  
3. <span data-ttu-id="48519-131">Schedule</span><span class="sxs-lookup"><span data-stu-id="48519-131">Schedule</span></span>  
4. <span data-ttu-id="48519-132">History</span><span class="sxs-lookup"><span data-stu-id="48519-132">History</span></span>
5. <span data-ttu-id="48519-133">Users</span><span class="sxs-lookup"><span data-stu-id="48519-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="48519-134">Properties</span><span class="sxs-lookup"><span data-stu-id="48519-134">Properties</span></span>
<span data-ttu-id="48519-135">These read-only properties describe the management metadata for the Scheduler job.</span><span class="sxs-lookup"><span data-stu-id="48519-135">These read-only properties describe the management metadata for the Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="48519-136">Action settings</span><span class="sxs-lookup"><span data-stu-id="48519-136">Action settings</span></span>
<span data-ttu-id="48519-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span><span class="sxs-lookup"><span data-stu-id="48519-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span></span> <span data-ttu-id="48519-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span><span class="sxs-lookup"><span data-stu-id="48519-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span></span>

<span data-ttu-id="48519-139">For all action types, you may change the retry policy and the error action.</span><span class="sxs-lookup"><span data-stu-id="48519-139">For all action types, you may change the retry policy and the error action.</span></span>

<span data-ttu-id="48519-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span><span class="sxs-lookup"><span data-stu-id="48519-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span></span> <span data-ttu-id="48519-141">You may also add, delete, or change the headers and basic authentication information.</span><span class="sxs-lookup"><span data-stu-id="48519-141">You may also add, delete, or change the headers and basic authentication information.</span></span>

<span data-ttu-id="48519-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span><span class="sxs-lookup"><span data-stu-id="48519-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="48519-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span><span class="sxs-lookup"><span data-stu-id="48519-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="48519-144">Schedule</span><span class="sxs-lookup"><span data-stu-id="48519-144">Schedule</span></span>
<span data-ttu-id="48519-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span><span class="sxs-lookup"><span data-stu-id="48519-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span></span>

<span data-ttu-id="48519-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="48519-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="48519-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span><span class="sxs-lookup"><span data-stu-id="48519-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="48519-148">History</span><span class="sxs-lookup"><span data-stu-id="48519-148">History</span></span>
<span data-ttu-id="48519-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span><span class="sxs-lookup"><span data-stu-id="48519-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span></span> <span data-ttu-id="48519-150">These metrics provide real-time values regarding the health of your Scheduler:</span><span class="sxs-lookup"><span data-stu-id="48519-150">These metrics provide real-time values regarding the health of your Scheduler:</span></span>

1. <span data-ttu-id="48519-151">Status</span><span class="sxs-lookup"><span data-stu-id="48519-151">Status</span></span>  
2. <span data-ttu-id="48519-152">Details</span><span class="sxs-lookup"><span data-stu-id="48519-152">Details</span></span>  
3. <span data-ttu-id="48519-153">Retry attempts</span><span class="sxs-lookup"><span data-stu-id="48519-153">Retry attempts</span></span>
4. <span data-ttu-id="48519-154">Occurrence: 1st, 2nd, 3rd, etc.</span><span class="sxs-lookup"><span data-stu-id="48519-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="48519-155">Start time of execution</span><span class="sxs-lookup"><span data-stu-id="48519-155">Start time of execution</span></span>  
6. <span data-ttu-id="48519-156">End time of execution</span><span class="sxs-lookup"><span data-stu-id="48519-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="48519-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span><span class="sxs-lookup"><span data-stu-id="48519-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span></span> <span data-ttu-id="48519-158">This dialog box also allows you to copy the response to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="48519-158">This dialog box also allows you to copy the response to the clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="48519-159">Users</span><span class="sxs-lookup"><span data-stu-id="48519-159">Users</span></span>
<span data-ttu-id="48519-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="48519-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="48519-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="48519-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="48519-162">See also</span><span class="sxs-lookup"><span data-stu-id="48519-162">See also</span></span>
 [<span data-ttu-id="48519-163">What is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="48519-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="48519-164">Scheduler concepts, terminology, and entity hierarchy</span><span class="sxs-lookup"><span data-stu-id="48519-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="48519-165">Plans and billing in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="48519-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="48519-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="48519-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="48519-167">Scheduler REST API reference</span><span class="sxs-lookup"><span data-stu-id="48519-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="48519-168">Scheduler PowerShell cmdlets reference</span><span class="sxs-lookup"><span data-stu-id="48519-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="48519-169">Scheduler high-availability and reliability</span><span class="sxs-lookup"><span data-stu-id="48519-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="48519-170">Scheduler limits, defaults, and error codes</span><span class="sxs-lookup"><span data-stu-id="48519-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="48519-171">Scheduler outbound authentication</span><span class="sxs-lookup"><span data-stu-id="48519-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/scheduler/media/scheduler-get-started-portal/scheduler-get-started-portal015.png
























