---
title: Autoscaling and App Service Environment v1
description: Autoscaling and App Service Environment
services: app-service
documentationcenter: ''
author: btardif
manager: erikre
editor: ''
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 0feb6e4862f643c35a58c0321181bdda22b032e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869193"
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="e6295-103">Autoscaling and App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="e6295-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="e6295-104">This article is about the App Service Environment v1.</span><span class="sxs-lookup"><span data-stu-id="e6295-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="e6295-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e6295-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="e6295-106">To learn more about the new version start with the [Introduction to the App  Service Environment](intro.md).</span><span class="sxs-lookup"><span data-stu-id="e6295-106">To learn more about the new version start with the [Introduction to the App  Service Environment](intro.md).</span></span>
> 

<span data-ttu-id="e6295-107">Azure App Service environments support *autoscaling*.</span><span class="sxs-lookup"><span data-stu-id="e6295-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="e6295-108">You can autoscale individual worker pools based on metrics or schedule.</span><span class="sxs-lookup"><span data-stu-id="e6295-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Autoscale options for a worker pool.][intro]

<span data-ttu-id="e6295-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span><span class="sxs-lookup"><span data-stu-id="e6295-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="e6295-111">Configure worker pool autoscale</span><span class="sxs-lookup"><span data-stu-id="e6295-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="e6295-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span><span class="sxs-lookup"><span data-stu-id="e6295-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Settings tab of the worker pool.][settings-scale]

<span data-ttu-id="e6295-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="e6295-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Manual scale settings.][scale-manual]

<span data-ttu-id="e6295-116">You can also configure an autoscale profile.</span><span class="sxs-lookup"><span data-stu-id="e6295-116">You can also configure an autoscale profile.</span></span>

![Autoscale settings.][scale-profile]

<span data-ttu-id="e6295-118">Autoscale profiles are useful to set limits on your scale.</span><span class="sxs-lookup"><span data-stu-id="e6295-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="e6295-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span><span class="sxs-lookup"><span data-stu-id="e6295-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Scale settings in profile.][scale-profile2]

<span data-ttu-id="e6295-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span><span class="sxs-lookup"><span data-stu-id="e6295-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="e6295-122">Autoscale rules are based on metrics.</span><span class="sxs-lookup"><span data-stu-id="e6295-122">Autoscale rules are based on metrics.</span></span>

![Scale rule.][scale-rule]

 <span data-ttu-id="e6295-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span><span class="sxs-lookup"><span data-stu-id="e6295-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="e6295-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span><span class="sxs-lookup"><span data-stu-id="e6295-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="e6295-126">Autoscale example</span><span class="sxs-lookup"><span data-stu-id="e6295-126">Autoscale example</span></span>
<span data-ttu-id="e6295-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span><span class="sxs-lookup"><span data-stu-id="e6295-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="e6295-128">This article explains all the necessary considerations when you set up autoscale.</span><span class="sxs-lookup"><span data-stu-id="e6295-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="e6295-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="e6295-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="e6295-130">Scenario introduction</span><span class="sxs-lookup"><span data-stu-id="e6295-130">Scenario introduction</span></span>
<span data-ttu-id="e6295-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span><span class="sxs-lookup"><span data-stu-id="e6295-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="e6295-132">The App Service environment is configured to manual scale as follows:</span><span class="sxs-lookup"><span data-stu-id="e6295-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="e6295-133">**Front ends:** 3</span><span class="sxs-lookup"><span data-stu-id="e6295-133">**Front ends:** 3</span></span>
* <span data-ttu-id="e6295-134">**Worker pool 1**: 10</span><span class="sxs-lookup"><span data-stu-id="e6295-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="e6295-135">**Worker pool 2**: 5</span><span class="sxs-lookup"><span data-stu-id="e6295-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="e6295-136">**Worker pool 3**: 5</span><span class="sxs-lookup"><span data-stu-id="e6295-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="e6295-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span><span class="sxs-lookup"><span data-stu-id="e6295-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="e6295-138">The App Service plans for QA and dev are configured to manual scale.</span><span class="sxs-lookup"><span data-stu-id="e6295-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="e6295-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span><span class="sxs-lookup"><span data-stu-id="e6295-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="e6295-140">Frank is very familiar with the application.</span><span class="sxs-lookup"><span data-stu-id="e6295-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="e6295-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span><span class="sxs-lookup"><span data-stu-id="e6295-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="e6295-142">Usage drops after that when users are done for that day.</span><span class="sxs-lookup"><span data-stu-id="e6295-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="e6295-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span><span class="sxs-lookup"><span data-stu-id="e6295-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="e6295-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span><span class="sxs-lookup"><span data-stu-id="e6295-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Specific settings for LOB app.][asp-scale]

| <span data-ttu-id="e6295-146">**Autoscale profile – Weekdays – App Service plan**</span><span class="sxs-lookup"><span data-stu-id="e6295-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="e6295-147">**Autoscale profile – Weekends – App Service plan**</span><span class="sxs-lookup"><span data-stu-id="e6295-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="e6295-148">**Name:** Weekday profile</span><span class="sxs-lookup"><span data-stu-id="e6295-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="e6295-149">**Name:** Weekend profile</span><span class="sxs-lookup"><span data-stu-id="e6295-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="e6295-150">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="e6295-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="e6295-151">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="e6295-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="e6295-152">**Profile:** Weekdays</span><span class="sxs-lookup"><span data-stu-id="e6295-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="e6295-153">**Profile:** Weekend</span><span class="sxs-lookup"><span data-stu-id="e6295-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="e6295-154">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="e6295-154">**Type:** Recurrence</span></span> |<span data-ttu-id="e6295-155">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="e6295-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="e6295-156">**Target range:** 5 to 20 instances</span><span class="sxs-lookup"><span data-stu-id="e6295-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="e6295-157">**Target range:** 3 to 10 instances</span><span class="sxs-lookup"><span data-stu-id="e6295-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="e6295-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span><span class="sxs-lookup"><span data-stu-id="e6295-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="e6295-159">**Days:** Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="e6295-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="e6295-160">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="e6295-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="e6295-161">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="e6295-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="e6295-162">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="e6295-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="e6295-163">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="e6295-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="e6295-164">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="e6295-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="e6295-165">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="e6295-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="e6295-166">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="e6295-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="e6295-167">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="e6295-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="e6295-168">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="e6295-168">**Metric:** CPU %</span></span> |<span data-ttu-id="e6295-169">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="e6295-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="e6295-170">**Operation:** Greater than 60%</span><span class="sxs-lookup"><span data-stu-id="e6295-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="e6295-171">**Operation:** Greater than 80%</span><span class="sxs-lookup"><span data-stu-id="e6295-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="e6295-172">**Duration:** 5 Minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="e6295-173">**Duration:** 10 Minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="e6295-174">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="e6295-175">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="e6295-176">**Action:** Increase count by 2</span><span class="sxs-lookup"><span data-stu-id="e6295-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="e6295-177">**Action:** Increase count by 1</span><span class="sxs-lookup"><span data-stu-id="e6295-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="e6295-178">**Cool down (minutes):** 15</span><span class="sxs-lookup"><span data-stu-id="e6295-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="e6295-179">**Cool down (minutes):** 20</span><span class="sxs-lookup"><span data-stu-id="e6295-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="e6295-180">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="e6295-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="e6295-181">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="e6295-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="e6295-182">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="e6295-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="e6295-183">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="e6295-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="e6295-184">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="e6295-184">**Metric:** CPU %</span></span> |<span data-ttu-id="e6295-185">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="e6295-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="e6295-186">**Operation:** Less than 30%</span><span class="sxs-lookup"><span data-stu-id="e6295-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="e6295-187">**Operation:** Less than 20%</span><span class="sxs-lookup"><span data-stu-id="e6295-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="e6295-188">**Duration:** 10 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="e6295-189">**Duration:** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="e6295-190">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="e6295-191">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="e6295-192">**Action:** Decrease count by 1</span><span class="sxs-lookup"><span data-stu-id="e6295-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="e6295-193">**Action:** Decrease count by 1</span><span class="sxs-lookup"><span data-stu-id="e6295-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="e6295-194">**Cool down (minutes):** 20</span><span class="sxs-lookup"><span data-stu-id="e6295-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="e6295-195">**Cool down (minutes):** 10</span><span class="sxs-lookup"><span data-stu-id="e6295-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="e6295-196">App Service plan inflation rate</span><span class="sxs-lookup"><span data-stu-id="e6295-196">App Service plan inflation rate</span></span>
<span data-ttu-id="e6295-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span><span class="sxs-lookup"><span data-stu-id="e6295-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="e6295-198">This rate can be calculated based on the values provided on the autoscale rule.</span><span class="sxs-lookup"><span data-stu-id="e6295-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="e6295-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span><span class="sxs-lookup"><span data-stu-id="e6295-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="e6295-200">The App Service plan inflation rate is calculated as follows:</span><span class="sxs-lookup"><span data-stu-id="e6295-200">The App Service plan inflation rate is calculated as follows:</span></span>

![App Service plan inflation rate calculation.][ASP-Inflation]

<span data-ttu-id="e6295-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span><span class="sxs-lookup"><span data-stu-id="e6295-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![App Service plan inflation rate for weekdays based on Autoscale – Scale Up rule.][Equation1]

<span data-ttu-id="e6295-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span><span class="sxs-lookup"><span data-stu-id="e6295-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![App Service plan inflation rate for weekends based on Autoscale – Scale Up rule.][Equation2]

<span data-ttu-id="e6295-206">This value can also be calculated for scale-down operations.</span><span class="sxs-lookup"><span data-stu-id="e6295-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="e6295-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span><span class="sxs-lookup"><span data-stu-id="e6295-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![App Service plan inflation rate for weekdays based on Autoscale – Scale Down rule.][Equation3]

<span data-ttu-id="e6295-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span><span class="sxs-lookup"><span data-stu-id="e6295-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![App Service plan inflation rate for weekends based on Autoscale – Scale Down rule.][Equation4]

<span data-ttu-id="e6295-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span><span class="sxs-lookup"><span data-stu-id="e6295-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="e6295-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span><span class="sxs-lookup"><span data-stu-id="e6295-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="e6295-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span><span class="sxs-lookup"><span data-stu-id="e6295-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Total inflation rate calculation for multiple App Service plans hosted in a worker pool.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="e6295-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span><span class="sxs-lookup"><span data-stu-id="e6295-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="e6295-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span><span class="sxs-lookup"><span data-stu-id="e6295-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="e6295-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span><span class="sxs-lookup"><span data-stu-id="e6295-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="e6295-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span><span class="sxs-lookup"><span data-stu-id="e6295-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="e6295-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="e6295-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="e6295-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span><span class="sxs-lookup"><span data-stu-id="e6295-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="e6295-221">With this information, Frank can define the following autoscale profile and rules:</span><span class="sxs-lookup"><span data-stu-id="e6295-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Autoscale profile rules for LOB example.][Worker-Pool-Scale]

| <span data-ttu-id="e6295-223">**Autoscale profile – Weekdays**</span><span class="sxs-lookup"><span data-stu-id="e6295-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="e6295-224">**Autoscale profile – Weekends**</span><span class="sxs-lookup"><span data-stu-id="e6295-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="e6295-225">**Name:** Weekday profile</span><span class="sxs-lookup"><span data-stu-id="e6295-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="e6295-226">**Name:** Weekend profile</span><span class="sxs-lookup"><span data-stu-id="e6295-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="e6295-227">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="e6295-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="e6295-228">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="e6295-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="e6295-229">**Profile:** Weekdays</span><span class="sxs-lookup"><span data-stu-id="e6295-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="e6295-230">**Profile:** Weekend</span><span class="sxs-lookup"><span data-stu-id="e6295-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="e6295-231">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="e6295-231">**Type:** Recurrence</span></span> |<span data-ttu-id="e6295-232">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="e6295-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="e6295-233">**Target range:** 13 to 25 instances</span><span class="sxs-lookup"><span data-stu-id="e6295-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="e6295-234">**Target range:** 6 to 15 instances</span><span class="sxs-lookup"><span data-stu-id="e6295-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="e6295-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span><span class="sxs-lookup"><span data-stu-id="e6295-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="e6295-236">**Days:** Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="e6295-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="e6295-237">**Start time:** 7:00 AM</span><span class="sxs-lookup"><span data-stu-id="e6295-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="e6295-238">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="e6295-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="e6295-239">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="e6295-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="e6295-240">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="e6295-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="e6295-241">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="e6295-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="e6295-242">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="e6295-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="e6295-243">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="e6295-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="e6295-244">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="e6295-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="e6295-245">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="e6295-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="e6295-246">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="e6295-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="e6295-247">**Operation:** Less than 8</span><span class="sxs-lookup"><span data-stu-id="e6295-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="e6295-248">**Operation:** Less than 3</span><span class="sxs-lookup"><span data-stu-id="e6295-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="e6295-249">**Duration:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="e6295-250">**Duration:** 30 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="e6295-251">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="e6295-252">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="e6295-253">**Action:** Increase count by 8</span><span class="sxs-lookup"><span data-stu-id="e6295-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="e6295-254">**Action:** Increase count by 3</span><span class="sxs-lookup"><span data-stu-id="e6295-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="e6295-255">**Cool down (minutes):** 180</span><span class="sxs-lookup"><span data-stu-id="e6295-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="e6295-256">**Cool down (minutes):** 180</span><span class="sxs-lookup"><span data-stu-id="e6295-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="e6295-257">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="e6295-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="e6295-258">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="e6295-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="e6295-259">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="e6295-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="e6295-260">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="e6295-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="e6295-261">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="e6295-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="e6295-262">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="e6295-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="e6295-263">**Operation:** Greater than 8</span><span class="sxs-lookup"><span data-stu-id="e6295-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="e6295-264">**Operation:** Greater than 3</span><span class="sxs-lookup"><span data-stu-id="e6295-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="e6295-265">**Duration:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="e6295-266">**Duration:** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="e6295-267">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="e6295-268">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="e6295-269">**Action:** Decrease count by 2</span><span class="sxs-lookup"><span data-stu-id="e6295-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="e6295-270">**Action:** Decrease count by 3</span><span class="sxs-lookup"><span data-stu-id="e6295-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="e6295-271">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="e6295-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="e6295-272">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="e6295-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="e6295-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span><span class="sxs-lookup"><span data-stu-id="e6295-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="e6295-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span><span class="sxs-lookup"><span data-stu-id="e6295-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="e6295-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span><span class="sxs-lookup"><span data-stu-id="e6295-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="e6295-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span><span class="sxs-lookup"><span data-stu-id="e6295-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="e6295-277">Autoscale for front-end pool</span><span class="sxs-lookup"><span data-stu-id="e6295-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="e6295-278">Rules for front-end autoscale are simpler than for worker pools.</span><span class="sxs-lookup"><span data-stu-id="e6295-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="e6295-279">Primarily, you should</span><span class="sxs-lookup"><span data-stu-id="e6295-279">Primarily, you should</span></span>  
<span data-ttu-id="e6295-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span><span class="sxs-lookup"><span data-stu-id="e6295-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="e6295-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span><span class="sxs-lookup"><span data-stu-id="e6295-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Autoscale settings for front-end pool.][Front-End-Scale]

| <span data-ttu-id="e6295-283">**Autoscale profile – Front ends**</span><span class="sxs-lookup"><span data-stu-id="e6295-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="e6295-284">**Name:** Autoscale – Front ends</span><span class="sxs-lookup"><span data-stu-id="e6295-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="e6295-285">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="e6295-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="e6295-286">**Profile:** Everyday</span><span class="sxs-lookup"><span data-stu-id="e6295-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="e6295-287">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="e6295-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="e6295-288">**Target range:** 3 to 10 instances</span><span class="sxs-lookup"><span data-stu-id="e6295-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="e6295-289">**Days:** Everyday</span><span class="sxs-lookup"><span data-stu-id="e6295-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="e6295-290">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="e6295-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="e6295-291">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="e6295-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="e6295-292">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="e6295-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="e6295-293">**Resource:** Front-end pool</span><span class="sxs-lookup"><span data-stu-id="e6295-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="e6295-294">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="e6295-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="e6295-295">**Operation:** Greater than 60%</span><span class="sxs-lookup"><span data-stu-id="e6295-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="e6295-296">**Duration:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="e6295-297">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="e6295-298">**Action:** Increase count by 3</span><span class="sxs-lookup"><span data-stu-id="e6295-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="e6295-299">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="e6295-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="e6295-300">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="e6295-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="e6295-301">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="e6295-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="e6295-302">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="e6295-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="e6295-303">**Operation:** Less than 30%</span><span class="sxs-lookup"><span data-stu-id="e6295-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="e6295-304">**Duration:** 20 Minutes</span><span class="sxs-lookup"><span data-stu-id="e6295-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="e6295-305">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="e6295-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="e6295-306">**Action:** Decrease count by 3</span><span class="sxs-lookup"><span data-stu-id="e6295-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="e6295-307">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="e6295-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
