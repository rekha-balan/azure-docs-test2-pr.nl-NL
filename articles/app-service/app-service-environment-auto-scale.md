---
title: Autoscaling and App Service Environment | Microsoft Docs
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
ms.date: 10/24/2016
ms.author: byvinyal
ms.openlocfilehash: 27b966b5d5ccdab8d9b9dcb67600cb44bbddd6fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556552"
---
# <a name="autoscaling-and-app-service-environment"></a><span data-ttu-id="30784-103">Autoscaling and App Service Environment</span><span class="sxs-lookup"><span data-stu-id="30784-103">Autoscaling and App Service Environment</span></span>
<span data-ttu-id="30784-104">Azure App Service environments support *autoscaling*.</span><span class="sxs-lookup"><span data-stu-id="30784-104">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="30784-105">You can autoscale individual worker pools based on metrics or schedule.</span><span class="sxs-lookup"><span data-stu-id="30784-105">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Autoscale options for a worker pool.][intro]

<span data-ttu-id="30784-107">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span><span class="sxs-lookup"><span data-stu-id="30784-107">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="30784-108">Configure worker pool autoscale</span><span class="sxs-lookup"><span data-stu-id="30784-108">Configure worker pool autoscale</span></span>
<span data-ttu-id="30784-109">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span><span class="sxs-lookup"><span data-stu-id="30784-109">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Settings tab of the worker pool.][settings-scale]

<span data-ttu-id="30784-111">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="30784-111">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Manual scale settings.][scale-manual]

<span data-ttu-id="30784-113">You can also configure an autoscale profile.</span><span class="sxs-lookup"><span data-stu-id="30784-113">You can also configure an autoscale profile.</span></span>

![Autoscale settings.][scale-profile]

<span data-ttu-id="30784-115">Autoscale profiles are useful to set limits on your scale.</span><span class="sxs-lookup"><span data-stu-id="30784-115">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="30784-116">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span><span class="sxs-lookup"><span data-stu-id="30784-116">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Scale settings in profile.][scale-profile2]

<span data-ttu-id="30784-118">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span><span class="sxs-lookup"><span data-stu-id="30784-118">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="30784-119">Autoscale rules are based on metrics.</span><span class="sxs-lookup"><span data-stu-id="30784-119">Autoscale rules are based on metrics.</span></span>

![Scale rule.][scale-rule]

 <span data-ttu-id="30784-121">Any worker pool or front-end metrics can be used to define autoscale rules.</span><span class="sxs-lookup"><span data-stu-id="30784-121">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="30784-122">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span><span class="sxs-lookup"><span data-stu-id="30784-122">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="30784-123">Autoscale example</span><span class="sxs-lookup"><span data-stu-id="30784-123">Autoscale example</span></span>
<span data-ttu-id="30784-124">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span><span class="sxs-lookup"><span data-stu-id="30784-124">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="30784-125">This article explains all the necessary considerations when you set up autoscale.</span><span class="sxs-lookup"><span data-stu-id="30784-125">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="30784-126">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="30784-126">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="30784-127">Scenario introduction</span><span class="sxs-lookup"><span data-stu-id="30784-127">Scenario introduction</span></span>
<span data-ttu-id="30784-128">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span><span class="sxs-lookup"><span data-stu-id="30784-128">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="30784-129">The App Service environment is configured to manual scale as follows:</span><span class="sxs-lookup"><span data-stu-id="30784-129">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="30784-130">**Front ends:** 3</span><span class="sxs-lookup"><span data-stu-id="30784-130">**Front ends:** 3</span></span>
* <span data-ttu-id="30784-131">**Worker pool 1**: 10</span><span class="sxs-lookup"><span data-stu-id="30784-131">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="30784-132">**Worker pool 2**: 5</span><span class="sxs-lookup"><span data-stu-id="30784-132">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="30784-133">**Worker pool 3**: 5</span><span class="sxs-lookup"><span data-stu-id="30784-133">**Worker pool 3**: 5</span></span>

<span data-ttu-id="30784-134">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span><span class="sxs-lookup"><span data-stu-id="30784-134">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="30784-135">The App Service plans for QA and dev are configured to manual scale.</span><span class="sxs-lookup"><span data-stu-id="30784-135">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="30784-136">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span><span class="sxs-lookup"><span data-stu-id="30784-136">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="30784-137">Frank is very familiar with the application.</span><span class="sxs-lookup"><span data-stu-id="30784-137">Frank is very familiar with the application.</span></span> <span data-ttu-id="30784-138">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span><span class="sxs-lookup"><span data-stu-id="30784-138">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="30784-139">Usage drops after that when users are done for that day.</span><span class="sxs-lookup"><span data-stu-id="30784-139">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="30784-140">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span><span class="sxs-lookup"><span data-stu-id="30784-140">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="30784-141">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span><span class="sxs-lookup"><span data-stu-id="30784-141">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Specific settings for LOB app.][asp-scale]

| <span data-ttu-id="30784-143">**Autoscale profile – Weekdays – App Service plan**</span><span class="sxs-lookup"><span data-stu-id="30784-143">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="30784-144">**Autoscale profile – Weekends – App Service plan**</span><span class="sxs-lookup"><span data-stu-id="30784-144">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="30784-145">**Name:** Weekday profile</span><span class="sxs-lookup"><span data-stu-id="30784-145">**Name:** Weekday profile</span></span> |<span data-ttu-id="30784-146">**Name:** Weekend profile</span><span class="sxs-lookup"><span data-stu-id="30784-146">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="30784-147">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="30784-147">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="30784-148">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="30784-148">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="30784-149">**Profile:** Weekdays</span><span class="sxs-lookup"><span data-stu-id="30784-149">**Profile:** Weekdays</span></span> |<span data-ttu-id="30784-150">**Profile:** Weekend</span><span class="sxs-lookup"><span data-stu-id="30784-150">**Profile:** Weekend</span></span> |
| <span data-ttu-id="30784-151">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="30784-151">**Type:** Recurrence</span></span> |<span data-ttu-id="30784-152">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="30784-152">**Type:** Recurrence</span></span> |
| <span data-ttu-id="30784-153">**Target range:** 5 to 20 instances</span><span class="sxs-lookup"><span data-stu-id="30784-153">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="30784-154">**Target range:** 3 to 10 instances</span><span class="sxs-lookup"><span data-stu-id="30784-154">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="30784-155">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span><span class="sxs-lookup"><span data-stu-id="30784-155">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="30784-156">**Days:** Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="30784-156">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="30784-157">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="30784-157">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="30784-158">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="30784-158">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="30784-159">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="30784-159">**Time zone:** UTC-08</span></span> |<span data-ttu-id="30784-160">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="30784-160">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="30784-161">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="30784-161">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="30784-162">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="30784-162">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="30784-163">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="30784-163">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="30784-164">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="30784-164">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="30784-165">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="30784-165">**Metric:** CPU %</span></span> |<span data-ttu-id="30784-166">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="30784-166">**Metric:** CPU %</span></span> |
| <span data-ttu-id="30784-167">**Operation:** Greater than 60%</span><span class="sxs-lookup"><span data-stu-id="30784-167">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="30784-168">**Operation:** Greater than 80%</span><span class="sxs-lookup"><span data-stu-id="30784-168">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="30784-169">**Duration:** 5 Minutes</span><span class="sxs-lookup"><span data-stu-id="30784-169">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="30784-170">**Duration:** 10 Minutes</span><span class="sxs-lookup"><span data-stu-id="30784-170">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="30784-171">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-171">**Time aggregation:** Average</span></span> |<span data-ttu-id="30784-172">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-172">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="30784-173">**Action:** Increase count by 2</span><span class="sxs-lookup"><span data-stu-id="30784-173">**Action:** Increase count by 2</span></span> |<span data-ttu-id="30784-174">**Action:** Increase count by 1</span><span class="sxs-lookup"><span data-stu-id="30784-174">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="30784-175">**Cool down (minutes):** 15</span><span class="sxs-lookup"><span data-stu-id="30784-175">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="30784-176">**Cool down (minutes):** 20</span><span class="sxs-lookup"><span data-stu-id="30784-176">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="30784-177">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="30784-177">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="30784-178">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="30784-178">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="30784-179">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="30784-179">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="30784-180">**Resource:** Production (App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="30784-180">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="30784-181">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="30784-181">**Metric:** CPU %</span></span> |<span data-ttu-id="30784-182">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="30784-182">**Metric:** CPU %</span></span> |
| <span data-ttu-id="30784-183">**Operation:** Less than 30%</span><span class="sxs-lookup"><span data-stu-id="30784-183">**Operation:** Less than 30%</span></span> |<span data-ttu-id="30784-184">**Operation:** Less than 20%</span><span class="sxs-lookup"><span data-stu-id="30784-184">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="30784-185">**Duration:** 10 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-185">**Duration:** 10 minutes</span></span> |<span data-ttu-id="30784-186">**Duration:** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-186">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="30784-187">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-187">**Time aggregation:** Average</span></span> |<span data-ttu-id="30784-188">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-188">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="30784-189">**Action:** Decrease count by 1</span><span class="sxs-lookup"><span data-stu-id="30784-189">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="30784-190">**Action:** Decrease count by 1</span><span class="sxs-lookup"><span data-stu-id="30784-190">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="30784-191">**Cool down (minutes):** 20</span><span class="sxs-lookup"><span data-stu-id="30784-191">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="30784-192">**Cool down (minutes):** 10</span><span class="sxs-lookup"><span data-stu-id="30784-192">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="30784-193">App Service plan inflation rate</span><span class="sxs-lookup"><span data-stu-id="30784-193">App Service plan inflation rate</span></span>
<span data-ttu-id="30784-194">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span><span class="sxs-lookup"><span data-stu-id="30784-194">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="30784-195">This rate can be calculated based on the values provided on the autoscale rule.</span><span class="sxs-lookup"><span data-stu-id="30784-195">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="30784-196">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span><span class="sxs-lookup"><span data-stu-id="30784-196">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="30784-197">The App Service plan inflation rate is calculated as follows:</span><span class="sxs-lookup"><span data-stu-id="30784-197">The App Service plan inflation rate is calculated as follows:</span></span>

![App Service plan inflation rate calculation.][ASP-Inflation]

<span data-ttu-id="30784-199">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span><span class="sxs-lookup"><span data-stu-id="30784-199">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![App Service plan inflation rate for weekdays based on Autoscale – Scale Up rule.][Equation1]

<span data-ttu-id="30784-201">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span><span class="sxs-lookup"><span data-stu-id="30784-201">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![App Service plan inflation rate for weekends based on Autoscale – Scale Up rule.][Equation2]

<span data-ttu-id="30784-203">This value can also be calculated for scale-down operations.</span><span class="sxs-lookup"><span data-stu-id="30784-203">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="30784-204">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span><span class="sxs-lookup"><span data-stu-id="30784-204">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![App Service plan inflation rate for weekdays based on Autoscale – Scale Down rule.][Equation3]

<span data-ttu-id="30784-206">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span><span class="sxs-lookup"><span data-stu-id="30784-206">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![App Service plan inflation rate for weekends based on Autoscale – Scale Down rule.][Equation4]

<span data-ttu-id="30784-208">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span><span class="sxs-lookup"><span data-stu-id="30784-208">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="30784-209">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span><span class="sxs-lookup"><span data-stu-id="30784-209">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="30784-210">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span><span class="sxs-lookup"><span data-stu-id="30784-210">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Total inflation rate calculation for multiple App Service plans hosted in a worker pool.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="30784-212">Use the App Service plan inflation rate to define worker pool autoscale rules</span><span class="sxs-lookup"><span data-stu-id="30784-212">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="30784-213">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span><span class="sxs-lookup"><span data-stu-id="30784-213">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="30784-214">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span><span class="sxs-lookup"><span data-stu-id="30784-214">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="30784-215">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span><span class="sxs-lookup"><span data-stu-id="30784-215">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="30784-216">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="30784-216">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="30784-217">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span><span class="sxs-lookup"><span data-stu-id="30784-217">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="30784-218">With this information, Frank can define the following autoscale profile and rules:</span><span class="sxs-lookup"><span data-stu-id="30784-218">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Autoscale profile rules for LOB example.][Worker-Pool-Scale]

| <span data-ttu-id="30784-220">**Autoscale profile – Weekdays**</span><span class="sxs-lookup"><span data-stu-id="30784-220">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="30784-221">**Autoscale profile – Weekends**</span><span class="sxs-lookup"><span data-stu-id="30784-221">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="30784-222">**Name:** Weekday profile</span><span class="sxs-lookup"><span data-stu-id="30784-222">**Name:** Weekday profile</span></span> |<span data-ttu-id="30784-223">**Name:** Weekend profile</span><span class="sxs-lookup"><span data-stu-id="30784-223">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="30784-224">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="30784-224">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="30784-225">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="30784-225">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="30784-226">**Profile:** Weekdays</span><span class="sxs-lookup"><span data-stu-id="30784-226">**Profile:** Weekdays</span></span> |<span data-ttu-id="30784-227">**Profile:** Weekend</span><span class="sxs-lookup"><span data-stu-id="30784-227">**Profile:** Weekend</span></span> |
| <span data-ttu-id="30784-228">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="30784-228">**Type:** Recurrence</span></span> |<span data-ttu-id="30784-229">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="30784-229">**Type:** Recurrence</span></span> |
| <span data-ttu-id="30784-230">**Target range:** 13 to 25 instances</span><span class="sxs-lookup"><span data-stu-id="30784-230">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="30784-231">**Target range:** 6 to 15 instances</span><span class="sxs-lookup"><span data-stu-id="30784-231">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="30784-232">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span><span class="sxs-lookup"><span data-stu-id="30784-232">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="30784-233">**Days:** Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="30784-233">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="30784-234">**Start time:** 7:00 AM</span><span class="sxs-lookup"><span data-stu-id="30784-234">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="30784-235">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="30784-235">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="30784-236">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="30784-236">**Time zone:** UTC-08</span></span> |<span data-ttu-id="30784-237">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="30784-237">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="30784-238">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="30784-238">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="30784-239">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="30784-239">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="30784-240">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="30784-240">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="30784-241">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="30784-241">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="30784-242">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="30784-242">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="30784-243">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="30784-243">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="30784-244">**Operation:** Less than 8</span><span class="sxs-lookup"><span data-stu-id="30784-244">**Operation:** Less than 8</span></span> |<span data-ttu-id="30784-245">**Operation:** Less than 3</span><span class="sxs-lookup"><span data-stu-id="30784-245">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="30784-246">**Duration:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-246">**Duration:** 20 minutes</span></span> |<span data-ttu-id="30784-247">**Duration:** 30 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-247">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="30784-248">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-248">**Time aggregation:** Average</span></span> |<span data-ttu-id="30784-249">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-249">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="30784-250">**Action:** Increase count by 8</span><span class="sxs-lookup"><span data-stu-id="30784-250">**Action:** Increase count by 8</span></span> |<span data-ttu-id="30784-251">**Action:** Increase count by 3</span><span class="sxs-lookup"><span data-stu-id="30784-251">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="30784-252">**Cool down (minutes):** 180</span><span class="sxs-lookup"><span data-stu-id="30784-252">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="30784-253">**Cool down (minutes):** 180</span><span class="sxs-lookup"><span data-stu-id="30784-253">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="30784-254">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="30784-254">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="30784-255">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="30784-255">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="30784-256">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="30784-256">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="30784-257">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="30784-257">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="30784-258">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="30784-258">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="30784-259">**Metric:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="30784-259">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="30784-260">**Operation:** Greater than 8</span><span class="sxs-lookup"><span data-stu-id="30784-260">**Operation:** Greater than 8</span></span> |<span data-ttu-id="30784-261">**Operation:** Greater than 3</span><span class="sxs-lookup"><span data-stu-id="30784-261">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="30784-262">**Duration:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-262">**Duration:** 20 minutes</span></span> |<span data-ttu-id="30784-263">**Duration:** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-263">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="30784-264">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-264">**Time aggregation:** Average</span></span> |<span data-ttu-id="30784-265">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-265">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="30784-266">**Action:** Decrease count by 2</span><span class="sxs-lookup"><span data-stu-id="30784-266">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="30784-267">**Action:** Decrease count by 3</span><span class="sxs-lookup"><span data-stu-id="30784-267">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="30784-268">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="30784-268">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="30784-269">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="30784-269">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="30784-270">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span><span class="sxs-lookup"><span data-stu-id="30784-270">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="30784-271">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span><span class="sxs-lookup"><span data-stu-id="30784-271">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="30784-272">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span><span class="sxs-lookup"><span data-stu-id="30784-272">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="30784-273">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span><span class="sxs-lookup"><span data-stu-id="30784-273">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="30784-274">Autoscale for front-end pool</span><span class="sxs-lookup"><span data-stu-id="30784-274">Autoscale for front-end pool</span></span>
<span data-ttu-id="30784-275">Rules for front-end autoscale are simpler than for worker pools.</span><span class="sxs-lookup"><span data-stu-id="30784-275">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="30784-276">Primarily, you should</span><span class="sxs-lookup"><span data-stu-id="30784-276">Primarily, you should</span></span>  
<span data-ttu-id="30784-277">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span><span class="sxs-lookup"><span data-stu-id="30784-277">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="30784-278">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span><span class="sxs-lookup"><span data-stu-id="30784-278">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Autoscale settings for front-end pool.][Front-End-Scale]

| <span data-ttu-id="30784-280">**Autoscale profile – Front ends**</span><span class="sxs-lookup"><span data-stu-id="30784-280">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="30784-281">**Name:** Autoscale – Front ends</span><span class="sxs-lookup"><span data-stu-id="30784-281">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="30784-282">**Scale by:** Schedule and performance rules</span><span class="sxs-lookup"><span data-stu-id="30784-282">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="30784-283">**Profile:** Everyday</span><span class="sxs-lookup"><span data-stu-id="30784-283">**Profile:** Everyday</span></span> |
| <span data-ttu-id="30784-284">**Type:** Recurrence</span><span class="sxs-lookup"><span data-stu-id="30784-284">**Type:** Recurrence</span></span> |
| <span data-ttu-id="30784-285">**Target range:** 3 to 10 instances</span><span class="sxs-lookup"><span data-stu-id="30784-285">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="30784-286">**Days:** Everyday</span><span class="sxs-lookup"><span data-stu-id="30784-286">**Days:** Everyday</span></span> |
| <span data-ttu-id="30784-287">**Start time:** 9:00 AM</span><span class="sxs-lookup"><span data-stu-id="30784-287">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="30784-288">**Time zone:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="30784-288">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="30784-289">**Autoscale rule (Scale Up)**</span><span class="sxs-lookup"><span data-stu-id="30784-289">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="30784-290">**Resource:** Front-end pool</span><span class="sxs-lookup"><span data-stu-id="30784-290">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="30784-291">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="30784-291">**Metric:** CPU %</span></span> |
| <span data-ttu-id="30784-292">**Operation:** Greater than 60%</span><span class="sxs-lookup"><span data-stu-id="30784-292">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="30784-293">**Duration:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="30784-293">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="30784-294">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-294">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="30784-295">**Action:** Increase count by 3</span><span class="sxs-lookup"><span data-stu-id="30784-295">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="30784-296">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="30784-296">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="30784-297">**Autoscale rule (Scale Down)**</span><span class="sxs-lookup"><span data-stu-id="30784-297">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="30784-298">**Resource:** Worker pool 1</span><span class="sxs-lookup"><span data-stu-id="30784-298">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="30784-299">**Metric:** CPU %</span><span class="sxs-lookup"><span data-stu-id="30784-299">**Metric:** CPU %</span></span> |
| <span data-ttu-id="30784-300">**Operation:** Less than 30%</span><span class="sxs-lookup"><span data-stu-id="30784-300">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="30784-301">**Duration:** 20 Minutes</span><span class="sxs-lookup"><span data-stu-id="30784-301">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="30784-302">**Time aggregation:** Average</span><span class="sxs-lookup"><span data-stu-id="30784-302">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="30784-303">**Action:** Decrease count by 3</span><span class="sxs-lookup"><span data-stu-id="30784-303">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="30784-304">**Cool down (minutes):** 120</span><span class="sxs-lookup"><span data-stu-id="30784-304">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/introduction.png
[settings-scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/equation1.png
[Equation2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/equation2.png
[Equation3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/equation3.png
[Equation4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/app-service-environment-auto-scale/fe-scale.png















