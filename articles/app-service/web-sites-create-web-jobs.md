---
title: Run Background tasks with WebJobs in Azure App Service
description: Learn how to use WebJobs to run background tasks in Azure App Service web apps, API apps, or mobile apps.
services: app-service
documentationcenter: ''
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/09/2017
ms.author: glenga;david.ebbo;suwatch;pbatum;naren.soni
ms.openlocfilehash: c3a41733dd193d10349a0126bfa9c25ce4ba56e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857361"
---
# <a name="run-background-tasks-with-webjobs-in-azure-app-service"></a><span data-ttu-id="90a13-103">Run Background tasks with WebJobs in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="90a13-103">Run Background tasks with WebJobs in Azure App Service</span></span>

## <a name="overview"></a><span data-ttu-id="90a13-104">Overview</span><span class="sxs-lookup"><span data-stu-id="90a13-104">Overview</span></span>
<span data-ttu-id="90a13-105">WebJobs is a feature of [Azure App Service](https://docs.microsoft.com/azure/app-service/) that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="90a13-105">WebJobs is a feature of [Azure App Service](https://docs.microsoft.com/azure/app-service/) that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="90a13-106">There is no additional cost to use WebJobs.</span><span class="sxs-lookup"><span data-stu-id="90a13-106">There is no additional cost to use WebJobs.</span></span>

<span data-ttu-id="90a13-107">This article shows how to deploy WebJobs by using the [Azure portal](https://portal.azure.com) to upload an executable or script.</span><span class="sxs-lookup"><span data-stu-id="90a13-107">This article shows how to deploy WebJobs by using the [Azure portal](https://portal.azure.com) to upload an executable or script.</span></span> <span data-ttu-id="90a13-108">For information about how to develop and deploy WebJobs by using Visual Studio, see [Deploy WebJobs using Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="90a13-108">For information about how to develop and deploy WebJobs by using Visual Studio, see [Deploy WebJobs using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="90a13-109">The Azure WebJobs SDK can be used with WebJobs to simplify many programming tasks.</span><span class="sxs-lookup"><span data-stu-id="90a13-109">The Azure WebJobs SDK can be used with WebJobs to simplify many programming tasks.</span></span> <span data-ttu-id="90a13-110">For more information, see [What is the WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span><span class="sxs-lookup"><span data-stu-id="90a13-110">For more information, see [What is the WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span></span>

<span data-ttu-id="90a13-111">Azure Functions provides another way to run programs and scripts.</span><span class="sxs-lookup"><span data-stu-id="90a13-111">Azure Functions provides another way to run programs and scripts.</span></span> <span data-ttu-id="90a13-112">For a comparison between WebJobs and Functions, see [Choose between Flow, Logic Apps, Functions, and WebJobs](../azure-functions/functions-compare-logic-apps-ms-flow-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="90a13-112">For a comparison between WebJobs and Functions, see [Choose between Flow, Logic Apps, Functions, and WebJobs](../azure-functions/functions-compare-logic-apps-ms-flow-webjobs.md).</span></span>

## <a name="webjob-types"></a><span data-ttu-id="90a13-113">WebJob types</span><span class="sxs-lookup"><span data-stu-id="90a13-113">WebJob types</span></span>

<span data-ttu-id="90a13-114">The following table describes the differences between *continuous* and *triggered* WebJobs.</span><span class="sxs-lookup"><span data-stu-id="90a13-114">The following table describes the differences between *continuous* and *triggered* WebJobs.</span></span>


|<span data-ttu-id="90a13-115">Continuous</span><span class="sxs-lookup"><span data-stu-id="90a13-115">Continuous</span></span>  |<span data-ttu-id="90a13-116">Triggered</span><span class="sxs-lookup"><span data-stu-id="90a13-116">Triggered</span></span>  |
|---------|---------|
| <span data-ttu-id="90a13-117">Starts immediately when the WebJob is created.</span><span class="sxs-lookup"><span data-stu-id="90a13-117">Starts immediately when the WebJob is created.</span></span> <span data-ttu-id="90a13-118">To keep the job from ending, the program or script typically does its work inside an endless loop.</span><span class="sxs-lookup"><span data-stu-id="90a13-118">To keep the job from ending, the program or script typically does its work inside an endless loop.</span></span> <span data-ttu-id="90a13-119">If the job does end, you can restart it.</span><span class="sxs-lookup"><span data-stu-id="90a13-119">If the job does end, you can restart it.</span></span> | <span data-ttu-id="90a13-120">Starts only when triggered manually or on a schedule.</span><span class="sxs-lookup"><span data-stu-id="90a13-120">Starts only when triggered manually or on a schedule.</span></span> |
| <span data-ttu-id="90a13-121">Runs on all instances that the web app runs on.</span><span class="sxs-lookup"><span data-stu-id="90a13-121">Runs on all instances that the web app runs on.</span></span> <span data-ttu-id="90a13-122">You can optionally restrict the WebJob to a single instance.</span><span class="sxs-lookup"><span data-stu-id="90a13-122">You can optionally restrict the WebJob to a single instance.</span></span> |<span data-ttu-id="90a13-123">Runs on a single instance that Azure selects for load balancing.</span><span class="sxs-lookup"><span data-stu-id="90a13-123">Runs on a single instance that Azure selects for load balancing.</span></span>|
| <span data-ttu-id="90a13-124">Supports remote debugging.</span><span class="sxs-lookup"><span data-stu-id="90a13-124">Supports remote debugging.</span></span> | <span data-ttu-id="90a13-125">Doesn't support remote debugging.</span><span class="sxs-lookup"><span data-stu-id="90a13-125">Doesn't support remote debugging.</span></span>|

> [!NOTE]
> <span data-ttu-id="90a13-126">A web app can time out after 20 minutes of inactivity.</span><span class="sxs-lookup"><span data-stu-id="90a13-126">A web app can time out after 20 minutes of inactivity.</span></span> <span data-ttu-id="90a13-127">Only requests to the scm (deployment) site or to the web app's pages in the portal reset the timer.</span><span class="sxs-lookup"><span data-stu-id="90a13-127">Only requests to the scm (deployment) site or to the web app's pages in the portal reset the timer.</span></span> <span data-ttu-id="90a13-128">Requests to the actual site don't reset the timer.</span><span class="sxs-lookup"><span data-stu-id="90a13-128">Requests to the actual site don't reset the timer.</span></span> <span data-ttu-id="90a13-129">If your app runs continuous or scheduled WebJobs, enable **Always On** to ensure that the WebJobs run reliably.</span><span class="sxs-lookup"><span data-stu-id="90a13-129">If your app runs continuous or scheduled WebJobs, enable **Always On** to ensure that the WebJobs run reliably.</span></span> <span data-ttu-id="90a13-130">This feature is available only in the Basic, Standard, and Premium [pricing tiers](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span><span class="sxs-lookup"><span data-stu-id="90a13-130">This feature is available only in the Basic, Standard, and Premium [pricing tiers](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span></span>

## <a name="acceptablefiles"></a><span data-ttu-id="90a13-131">Supported file types for scripts or programs</span><span class="sxs-lookup"><span data-stu-id="90a13-131">Supported file types for scripts or programs</span></span>

<span data-ttu-id="90a13-132">The following file types are supported:</span><span class="sxs-lookup"><span data-stu-id="90a13-132">The following file types are supported:</span></span>

* <span data-ttu-id="90a13-133">.cmd, .bat, .exe (using Windows cmd)</span><span class="sxs-lookup"><span data-stu-id="90a13-133">.cmd, .bat, .exe (using Windows cmd)</span></span>
* <span data-ttu-id="90a13-134">.ps1 (using PowerShell)</span><span class="sxs-lookup"><span data-stu-id="90a13-134">.ps1 (using PowerShell)</span></span>
* <span data-ttu-id="90a13-135">.sh (using Bash)</span><span class="sxs-lookup"><span data-stu-id="90a13-135">.sh (using Bash)</span></span>
* <span data-ttu-id="90a13-136">.php (using PHP)</span><span class="sxs-lookup"><span data-stu-id="90a13-136">.php (using PHP)</span></span>
* <span data-ttu-id="90a13-137">.py (using Python)</span><span class="sxs-lookup"><span data-stu-id="90a13-137">.py (using Python)</span></span>
* <span data-ttu-id="90a13-138">.js (using Node.js)</span><span class="sxs-lookup"><span data-stu-id="90a13-138">.js (using Node.js)</span></span>
* <span data-ttu-id="90a13-139">.jar (using Java)</span><span class="sxs-lookup"><span data-stu-id="90a13-139">.jar (using Java)</span></span>

## <a name="CreateContinuous"></a> <span data-ttu-id="90a13-140">Create a continuous WebJob</span><span class="sxs-lookup"><span data-stu-id="90a13-140">Create a continuous WebJob</span></span>

<!-- 
Several steps in the three "Create..." sections are identical; 
when making changes in one don't forget the other two.
-->

1. <span data-ttu-id="90a13-141">In the [Azure portal](https://portal.azure.com), go to the **App Service** page of your App Service web app, API app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="90a13-141">In the [Azure portal](https://portal.azure.com), go to the **App Service** page of your App Service web app, API app, or mobile app.</span></span>

2. <span data-ttu-id="90a13-142">Select **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="90a13-142">Select **WebJobs**.</span></span>

   ![Select WebJobs](./media/web-sites-create-web-jobs/select-webjobs.png)

2. <span data-ttu-id="90a13-144">In the **WebJobs** page, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="90a13-144">In the **WebJobs** page, select **Add**.</span></span>

    ![WebJob page](./media/web-sites-create-web-jobs/wjblade.png)

3. <span data-ttu-id="90a13-146">Use the **Add WebJob** settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="90a13-146">Use the **Add WebJob** settings as specified in the table.</span></span>

   ![Add WebJob page](./media/web-sites-create-web-jobs/addwjcontinuous.png)

   | <span data-ttu-id="90a13-148">Setting</span><span class="sxs-lookup"><span data-stu-id="90a13-148">Setting</span></span>      | <span data-ttu-id="90a13-149">Sample value</span><span class="sxs-lookup"><span data-stu-id="90a13-149">Sample value</span></span>   | <span data-ttu-id="90a13-150">Description</span><span class="sxs-lookup"><span data-stu-id="90a13-150">Description</span></span>  |
   | ------------ | ----------------- | ------------ |
   | <span data-ttu-id="90a13-151">**Name**</span><span class="sxs-lookup"><span data-stu-id="90a13-151">**Name**</span></span> | <span data-ttu-id="90a13-152">myContinuousWebJob</span><span class="sxs-lookup"><span data-stu-id="90a13-152">myContinuousWebJob</span></span> | <span data-ttu-id="90a13-153">A name that is unique within an App Service app.</span><span class="sxs-lookup"><span data-stu-id="90a13-153">A name that is unique within an App Service app.</span></span> <span data-ttu-id="90a13-154">Must start with a letter or a number and cannot contain special characters other than "-" and "_".</span><span class="sxs-lookup"><span data-stu-id="90a13-154">Must start with a letter or a number and cannot contain special characters other than "-" and "_".</span></span> |
   | <span data-ttu-id="90a13-155">**File Upload**</span><span class="sxs-lookup"><span data-stu-id="90a13-155">**File Upload**</span></span> | <span data-ttu-id="90a13-156">ConsoleApp.zip</span><span class="sxs-lookup"><span data-stu-id="90a13-156">ConsoleApp.zip</span></span> | <span data-ttu-id="90a13-157">A *.zip* file that contains your executable or script file as well as any supporting files needed to run the program or script.</span><span class="sxs-lookup"><span data-stu-id="90a13-157">A *.zip* file that contains your executable or script file as well as any supporting files needed to run the program or script.</span></span> <span data-ttu-id="90a13-158">The supported executable or script file types are listed in the [Supported file types](#acceptablefiles) section.</span><span class="sxs-lookup"><span data-stu-id="90a13-158">The supported executable or script file types are listed in the [Supported file types](#acceptablefiles) section.</span></span> |
   | <span data-ttu-id="90a13-159">**Type**</span><span class="sxs-lookup"><span data-stu-id="90a13-159">**Type**</span></span> | <span data-ttu-id="90a13-160">Continuous</span><span class="sxs-lookup"><span data-stu-id="90a13-160">Continuous</span></span> | <span data-ttu-id="90a13-161">The [WebJob types](#webjob-types) are described earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="90a13-161">The [WebJob types](#webjob-types) are described earlier in this article.</span></span> |
   | <span data-ttu-id="90a13-162">**Scale**</span><span class="sxs-lookup"><span data-stu-id="90a13-162">**Scale**</span></span> | <span data-ttu-id="90a13-163">Multi instance</span><span class="sxs-lookup"><span data-stu-id="90a13-163">Multi instance</span></span> | <span data-ttu-id="90a13-164">Available only for Continuous WebJobs.</span><span class="sxs-lookup"><span data-stu-id="90a13-164">Available only for Continuous WebJobs.</span></span> <span data-ttu-id="90a13-165">Determines whether the program or script runs on all instances or just one instance.</span><span class="sxs-lookup"><span data-stu-id="90a13-165">Determines whether the program or script runs on all instances or just one instance.</span></span> <span data-ttu-id="90a13-166">The option to run on multiple instances doesn't apply to the Free or Shared [pricing tiers](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span><span class="sxs-lookup"><span data-stu-id="90a13-166">The option to run on multiple instances doesn't apply to the Free or Shared [pricing tiers](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span></span> | 

4. <span data-ttu-id="90a13-167">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="90a13-167">Click **OK**.</span></span>

   <span data-ttu-id="90a13-168">The new WebJob appears on the **WebJobs** page.</span><span class="sxs-lookup"><span data-stu-id="90a13-168">The new WebJob appears on the **WebJobs** page.</span></span>

   ![List of WebJobs](./media/web-sites-create-web-jobs/listallwebjobs.png)

2. <span data-ttu-id="90a13-170">To stop or restart a continuous WebJob, right-click the WebJob in the list and click **Stop** or **Start**.</span><span class="sxs-lookup"><span data-stu-id="90a13-170">To stop or restart a continuous WebJob, right-click the WebJob in the list and click **Stop** or **Start**.</span></span>

    ![Stop a continuous WebJob](./media/web-sites-create-web-jobs/continuousstop.png)

## <a name="CreateOnDemand"></a> <span data-ttu-id="90a13-172">Create a manually triggered WebJob</span><span class="sxs-lookup"><span data-stu-id="90a13-172">Create a manually triggered WebJob</span></span>

<!-- 
Several steps in the three "Create..." sections are identical; 
when making changes in one don't forget the other two.
-->

1. <span data-ttu-id="90a13-173">In the [Azure portal](https://portal.azure.com), go to the **App Service** page of your App Service web app, API app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="90a13-173">In the [Azure portal](https://portal.azure.com), go to the **App Service** page of your App Service web app, API app, or mobile app.</span></span>

2. <span data-ttu-id="90a13-174">Select **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="90a13-174">Select **WebJobs**.</span></span>

   ![Select WebJobs](./media/web-sites-create-web-jobs/select-webjobs.png)

2. <span data-ttu-id="90a13-176">In the **WebJobs** page, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="90a13-176">In the **WebJobs** page, select **Add**.</span></span>

    ![WebJob page](./media/web-sites-create-web-jobs/wjblade.png)

3. <span data-ttu-id="90a13-178">Use the **Add WebJob** settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="90a13-178">Use the **Add WebJob** settings as specified in the table.</span></span>

   ![Add WebJob page](./media/web-sites-create-web-jobs/addwjtriggered.png)

   | <span data-ttu-id="90a13-180">Setting</span><span class="sxs-lookup"><span data-stu-id="90a13-180">Setting</span></span>      | <span data-ttu-id="90a13-181">Sample value</span><span class="sxs-lookup"><span data-stu-id="90a13-181">Sample value</span></span>   | <span data-ttu-id="90a13-182">Description</span><span class="sxs-lookup"><span data-stu-id="90a13-182">Description</span></span>  |
   | ------------ | ----------------- | ------------ |
   | <span data-ttu-id="90a13-183">**Name**</span><span class="sxs-lookup"><span data-stu-id="90a13-183">**Name**</span></span> | <span data-ttu-id="90a13-184">myTriggeredWebJob</span><span class="sxs-lookup"><span data-stu-id="90a13-184">myTriggeredWebJob</span></span> | <span data-ttu-id="90a13-185">A name that is unique within an App Service app.</span><span class="sxs-lookup"><span data-stu-id="90a13-185">A name that is unique within an App Service app.</span></span> <span data-ttu-id="90a13-186">Must start with a letter or a number and cannot contain special characters other than "-" and "_".</span><span class="sxs-lookup"><span data-stu-id="90a13-186">Must start with a letter or a number and cannot contain special characters other than "-" and "_".</span></span>|
   | <span data-ttu-id="90a13-187">**File Upload**</span><span class="sxs-lookup"><span data-stu-id="90a13-187">**File Upload**</span></span> | <span data-ttu-id="90a13-188">ConsoleApp.zip</span><span class="sxs-lookup"><span data-stu-id="90a13-188">ConsoleApp.zip</span></span> | <span data-ttu-id="90a13-189">A *.zip* file that contains your executable or script file as well as any supporting files needed to run the program or script.</span><span class="sxs-lookup"><span data-stu-id="90a13-189">A *.zip* file that contains your executable or script file as well as any supporting files needed to run the program or script.</span></span> <span data-ttu-id="90a13-190">The supported executable or script file types are listed in the [Supported file types](#acceptablefiles) section.</span><span class="sxs-lookup"><span data-stu-id="90a13-190">The supported executable or script file types are listed in the [Supported file types](#acceptablefiles) section.</span></span> |
   | <span data-ttu-id="90a13-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="90a13-191">**Type**</span></span> | <span data-ttu-id="90a13-192">Triggered</span><span class="sxs-lookup"><span data-stu-id="90a13-192">Triggered</span></span> | <span data-ttu-id="90a13-193">The [WebJob types](#webjob-types) are described earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="90a13-193">The [WebJob types](#webjob-types) are described earlier in this article.</span></span> |
   | <span data-ttu-id="90a13-194">**Triggers**</span><span class="sxs-lookup"><span data-stu-id="90a13-194">**Triggers**</span></span> | <span data-ttu-id="90a13-195">Manual</span><span class="sxs-lookup"><span data-stu-id="90a13-195">Manual</span></span> | |

4. <span data-ttu-id="90a13-196">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="90a13-196">Click **OK**.</span></span>

   <span data-ttu-id="90a13-197">The new WebJob appears on the **WebJobs** page.</span><span class="sxs-lookup"><span data-stu-id="90a13-197">The new WebJob appears on the **WebJobs** page.</span></span>

   ![List of WebJobs](./media/web-sites-create-web-jobs/listallwebjobs.png)

7. <span data-ttu-id="90a13-199">To run the WebJob, right-click its name in the list and click **Run**.</span><span class="sxs-lookup"><span data-stu-id="90a13-199">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Run WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateScheduledCRON"></a> <span data-ttu-id="90a13-201">Create a scheduled WebJob</span><span class="sxs-lookup"><span data-stu-id="90a13-201">Create a scheduled WebJob</span></span>

<!-- 
Several steps in the three "Create..." sections are identical; 
when making changes in one don't forget the other two.
-->

1. <span data-ttu-id="90a13-202">In the [Azure portal](https://portal.azure.com), go to the **App Service** page of your App Service web app, API app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="90a13-202">In the [Azure portal](https://portal.azure.com), go to the **App Service** page of your App Service web app, API app, or mobile app.</span></span>

2. <span data-ttu-id="90a13-203">Select **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="90a13-203">Select **WebJobs**.</span></span>

   ![Select WebJobs](./media/web-sites-create-web-jobs/select-webjobs.png)

2. <span data-ttu-id="90a13-205">In the **WebJobs** page, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="90a13-205">In the **WebJobs** page, select **Add**.</span></span>

   ![WebJob page](./media/web-sites-create-web-jobs/wjblade.png)

3. <span data-ttu-id="90a13-207">Use the **Add WebJob** settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="90a13-207">Use the **Add WebJob** settings as specified in the table.</span></span>

   ![Add WebJob page](./media/web-sites-create-web-jobs/addwjscheduled.png)

   | <span data-ttu-id="90a13-209">Setting</span><span class="sxs-lookup"><span data-stu-id="90a13-209">Setting</span></span>      | <span data-ttu-id="90a13-210">Sample value</span><span class="sxs-lookup"><span data-stu-id="90a13-210">Sample value</span></span>   | <span data-ttu-id="90a13-211">Description</span><span class="sxs-lookup"><span data-stu-id="90a13-211">Description</span></span>  |
   | ------------ | ----------------- | ------------ |
   | <span data-ttu-id="90a13-212">**Name**</span><span class="sxs-lookup"><span data-stu-id="90a13-212">**Name**</span></span> | <span data-ttu-id="90a13-213">myScheduledWebJob</span><span class="sxs-lookup"><span data-stu-id="90a13-213">myScheduledWebJob</span></span> | <span data-ttu-id="90a13-214">A name that is unique within an App Service app.</span><span class="sxs-lookup"><span data-stu-id="90a13-214">A name that is unique within an App Service app.</span></span> <span data-ttu-id="90a13-215">Must start with a letter or a number and cannot contain special characters other than "-" and "_".</span><span class="sxs-lookup"><span data-stu-id="90a13-215">Must start with a letter or a number and cannot contain special characters other than "-" and "_".</span></span> |
   | <span data-ttu-id="90a13-216">**File Upload**</span><span class="sxs-lookup"><span data-stu-id="90a13-216">**File Upload**</span></span> | <span data-ttu-id="90a13-217">ConsoleApp.zip</span><span class="sxs-lookup"><span data-stu-id="90a13-217">ConsoleApp.zip</span></span> | <span data-ttu-id="90a13-218">A *.zip* file that contains your executable or script file as well as any supporting files needed to run the program or script.</span><span class="sxs-lookup"><span data-stu-id="90a13-218">A *.zip* file that contains your executable or script file as well as any supporting files needed to run the program or script.</span></span> <span data-ttu-id="90a13-219">The supported executable or script file types are listed in the [Supported file types](#acceptablefiles) section.</span><span class="sxs-lookup"><span data-stu-id="90a13-219">The supported executable or script file types are listed in the [Supported file types](#acceptablefiles) section.</span></span> |
   | <span data-ttu-id="90a13-220">**Type**</span><span class="sxs-lookup"><span data-stu-id="90a13-220">**Type**</span></span> | <span data-ttu-id="90a13-221">Triggered</span><span class="sxs-lookup"><span data-stu-id="90a13-221">Triggered</span></span> | <span data-ttu-id="90a13-222">The [WebJob types](#webjob-types) are described earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="90a13-222">The [WebJob types](#webjob-types) are described earlier in this article.</span></span> |
   | <span data-ttu-id="90a13-223">**Triggers**</span><span class="sxs-lookup"><span data-stu-id="90a13-223">**Triggers**</span></span> | <span data-ttu-id="90a13-224">Scheduled</span><span class="sxs-lookup"><span data-stu-id="90a13-224">Scheduled</span></span> | <span data-ttu-id="90a13-225">For the scheduling to work reliably, enable the Always On feature.</span><span class="sxs-lookup"><span data-stu-id="90a13-225">For the scheduling to work reliably, enable the Always On feature.</span></span> <span data-ttu-id="90a13-226">Always On is available only in the Basic, Standard, and Premium pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="90a13-226">Always On is available only in the Basic, Standard, and Premium pricing tiers.</span></span>|
   | <span data-ttu-id="90a13-227">**CRON Expression**</span><span class="sxs-lookup"><span data-stu-id="90a13-227">**CRON Expression**</span></span> | <span data-ttu-id="90a13-228">0 0/20 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="90a13-228">0 0/20 \* \* \* \*</span></span> | <span data-ttu-id="90a13-229">[CRON expressions](#cron-expressions) are described in the following section.</span><span class="sxs-lookup"><span data-stu-id="90a13-229">[CRON expressions](#cron-expressions) are described in the following section.</span></span> |

4. <span data-ttu-id="90a13-230">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="90a13-230">Click **OK**.</span></span>

   <span data-ttu-id="90a13-231">The new WebJob appears on the **WebJobs** page.</span><span class="sxs-lookup"><span data-stu-id="90a13-231">The new WebJob appears on the **WebJobs** page.</span></span>

   ![List of WebJobs](./media/web-sites-create-web-jobs/listallwebjobs.png)

## <a name="cron-expressions"></a><span data-ttu-id="90a13-233">CRON expressions</span><span class="sxs-lookup"><span data-stu-id="90a13-233">CRON expressions</span></span>

<span data-ttu-id="90a13-234">You can enter a [CRON expression](../azure-functions/functions-bindings-timer.md#cron-expressions) in the portal or include a `settings.job` file at the root of your WebJob *.zip* file, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="90a13-234">You can enter a [CRON expression](../azure-functions/functions-bindings-timer.md#cron-expressions) in the portal or include a `settings.job` file at the root of your WebJob *.zip* file, as in the following example:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

> [!NOTE]
> <span data-ttu-id="90a13-235">When you deploy a WebJob from Visual Studio, mark your `settings.job` file properties as **Copy if newer**.</span><span class="sxs-lookup"><span data-stu-id="90a13-235">When you deploy a WebJob from Visual Studio, mark your `settings.job` file properties as **Copy if newer**.</span></span>

## <a name="ViewJobHistory"></a> <span data-ttu-id="90a13-236">View the job history</span><span class="sxs-lookup"><span data-stu-id="90a13-236">View the job history</span></span>

1. <span data-ttu-id="90a13-237">Select the WebJob you want to see history for, and then select the **Logs** button.</span><span class="sxs-lookup"><span data-stu-id="90a13-237">Select the WebJob you want to see history for, and then select the **Logs** button.</span></span>
   
   ![Logs button](./media/web-sites-create-web-jobs/wjbladelogslink.png)

2. <span data-ttu-id="90a13-239">In the **WebJob Details** page, select a time to see details for one run.</span><span class="sxs-lookup"><span data-stu-id="90a13-239">In the **WebJob Details** page, select a time to see details for one run.</span></span>
   
   ![WebJob Details](./media/web-sites-create-web-jobs/webjobdetails.png)

3. <span data-ttu-id="90a13-241">In the **WebJob Run Details** page, select **Toggle Output** to see the text of the log contents.</span><span class="sxs-lookup"><span data-stu-id="90a13-241">In the **WebJob Run Details** page, select **Toggle Output** to see the text of the log contents.</span></span>
   
    ![Web job run details](./media/web-sites-create-web-jobs/webjobrundetails.png)

   <span data-ttu-id="90a13-243">To see the output text in a separate browser window, select **download**.</span><span class="sxs-lookup"><span data-stu-id="90a13-243">To see the output text in a separate browser window, select **download**.</span></span> <span data-ttu-id="90a13-244">To download the text itself, right-click **download** and use your browser options to save the file contents.</span><span class="sxs-lookup"><span data-stu-id="90a13-244">To download the text itself, right-click **download** and use your browser options to save the file contents.</span></span>
   
5. <span data-ttu-id="90a13-245">Select the **WebJobs** breadcrumb link at the top of the page to go to a list of WebJobs.</span><span class="sxs-lookup"><span data-stu-id="90a13-245">Select the **WebJobs** breadcrumb link at the top of the page to go to a list of WebJobs.</span></span>

    ![WebJob breadcrumb](./media/web-sites-create-web-jobs/breadcrumb.png)
   
    ![List of WebJobs in history dashboard](./media/web-sites-create-web-jobs/webjobslist.png)
   
## <a name="NextSteps"></a> <span data-ttu-id="90a13-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="90a13-248">Next steps</span></span>

<span data-ttu-id="90a13-249">The Azure WebJobs SDK can be used with WebJobs to simplify many programming tasks.</span><span class="sxs-lookup"><span data-stu-id="90a13-249">The Azure WebJobs SDK can be used with WebJobs to simplify many programming tasks.</span></span> <span data-ttu-id="90a13-250">For more information, see [What is the WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span><span class="sxs-lookup"><span data-stu-id="90a13-250">For more information, see [What is the WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span></span>
