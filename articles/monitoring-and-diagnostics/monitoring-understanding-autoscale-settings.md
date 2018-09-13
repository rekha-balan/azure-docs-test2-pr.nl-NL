---
title: Understanding autoscale settings in Azure Monitor
description: A detailed breakdown of autoscale settings and how they work. Applies to Virtual Machines, Cloud Services, Web Apps
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 12/18/2017
ms.author: ancav
ms.component: autoscale
ms.openlocfilehash: 982bc43fd86a808da07833d77bde17e17789b2d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870509"
---
# <a name="understand-autoscale-settings"></a><span data-ttu-id="7cce5-104">Understand Autoscale settings</span><span class="sxs-lookup"><span data-stu-id="7cce5-104">Understand Autoscale settings</span></span>
<span data-ttu-id="7cce5-105">Autoscale settings help ensure that you have the right amount of resources running to handle the fluctuating load of your application.</span><span class="sxs-lookup"><span data-stu-id="7cce5-105">Autoscale settings help ensure that you have the right amount of resources running to handle the fluctuating load of your application.</span></span> <span data-ttu-id="7cce5-106">You can configure Autoscale settings to be triggered based on metrics that indicate load or performance, or triggered at a scheduled date and time.</span><span class="sxs-lookup"><span data-stu-id="7cce5-106">You can configure Autoscale settings to be triggered based on metrics that indicate load or performance, or triggered at a scheduled date and time.</span></span> <span data-ttu-id="7cce5-107">This article takes a detailed look at the anatomy of an Autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="7cce5-107">This article takes a detailed look at the anatomy of an Autoscale setting.</span></span> <span data-ttu-id="7cce5-108">The article begins with the schema and properties of a setting, and then walks through the different profile types that can be configured.</span><span class="sxs-lookup"><span data-stu-id="7cce5-108">The article begins with the schema and properties of a setting, and then walks through the different profile types that can be configured.</span></span> <span data-ttu-id="7cce5-109">Finally, the article discusses how the Autoscale feature in Azure evaluates which profile to execute at any given time.</span><span class="sxs-lookup"><span data-stu-id="7cce5-109">Finally, the article discusses how the Autoscale feature in Azure evaluates which profile to execute at any given time.</span></span>

## <a name="autoscale-setting-schema"></a><span data-ttu-id="7cce5-110">Autoscale setting schema</span><span class="sxs-lookup"><span data-stu-id="7cce5-110">Autoscale setting schema</span></span>
<span data-ttu-id="7cce5-111">To illustrate the Autoscale setting schema, the following Autoscale setting is used.</span><span class="sxs-lookup"><span data-stu-id="7cce5-111">To illustrate the Autoscale setting schema, the following Autoscale setting is used.</span></span> <span data-ttu-id="7cce5-112">It is important to note that this Autoscale setting has:</span><span class="sxs-lookup"><span data-stu-id="7cce5-112">It is important to note that this Autoscale setting has:</span></span>
- <span data-ttu-id="7cce5-113">One profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-113">One profile.</span></span> 
- <span data-ttu-id="7cce5-114">Two metric rules in this profile: one for scale out, and one for scale in.</span><span class="sxs-lookup"><span data-stu-id="7cce5-114">Two metric rules in this profile: one for scale out, and one for scale in.</span></span>
  - <span data-ttu-id="7cce5-115">The scale-out rule is triggered when the virtual machine scale set's average percentage CPU metric is greater than 85 percent for the past 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="7cce5-115">The scale-out rule is triggered when the virtual machine scale set's average percentage CPU metric is greater than 85 percent for the past 10 minutes.</span></span>
  - <span data-ttu-id="7cce5-116">The scale-in rule is triggered when the virtual machine scale set's average is less than 60 percent for the past minute.</span><span class="sxs-lookup"><span data-stu-id="7cce5-116">The scale-in rule is triggered when the virtual machine scale set's average is less than 60 percent for the past minute.</span></span>

> [!NOTE]
> <span data-ttu-id="7cce5-117">A setting can have multiple profiles.</span><span class="sxs-lookup"><span data-stu-id="7cce5-117">A setting can have multiple profiles.</span></span> <span data-ttu-id="7cce5-118">To learn more, see the [profiles](#autoscale-profiles) section.</span><span class="sxs-lookup"><span data-stu-id="7cce5-118">To learn more, see the [profiles](#autoscale-profiles) section.</span></span> <span data-ttu-id="7cce5-119">A profile can also have multiple scale-out rules and scale-in rules defined.</span><span class="sxs-lookup"><span data-stu-id="7cce5-119">A profile can also have multiple scale-out rules and scale-in rules defined.</span></span> <span data-ttu-id="7cce5-120">To see how they are evaluated, see the [evaluation](#autoscale-evaluation) section.</span><span class="sxs-lookup"><span data-stu-id="7cce5-120">To see how they are evaluated, see the [evaluation](#autoscale-evaluation) section.</span></span>

```JSON
{
  "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/setting1",
  "name": "setting1",
  "type": "Microsoft.Insights/autoscaleSettings",
  "location": "East US",
  "properties": {
    "enabled": true,
    "targetResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/vmss1",
    "profiles": [
      {
        "name": "mainProfile",
        "capacity": {
          "minimum": "1",
          "maximum": "4",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "Percentage CPU",
              "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/vmss1",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT10M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 85
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
    {
            "metricTrigger": {
              "metricName": "Percentage CPU",
              "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/vmss1",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT10M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 60
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ]
  }
}
```

| <span data-ttu-id="7cce5-121">Section</span><span class="sxs-lookup"><span data-stu-id="7cce5-121">Section</span></span> | <span data-ttu-id="7cce5-122">Element name</span><span class="sxs-lookup"><span data-stu-id="7cce5-122">Element name</span></span> | <span data-ttu-id="7cce5-123">Description</span><span class="sxs-lookup"><span data-stu-id="7cce5-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cce5-124">Setting</span><span class="sxs-lookup"><span data-stu-id="7cce5-124">Setting</span></span> | <span data-ttu-id="7cce5-125">ID</span><span class="sxs-lookup"><span data-stu-id="7cce5-125">ID</span></span> | <span data-ttu-id="7cce5-126">The Autoscale setting's resource ID.</span><span class="sxs-lookup"><span data-stu-id="7cce5-126">The Autoscale setting's resource ID.</span></span> <span data-ttu-id="7cce5-127">Autoscale settings are an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="7cce5-127">Autoscale settings are an Azure Resource Manager resource.</span></span> |
| <span data-ttu-id="7cce5-128">Setting</span><span class="sxs-lookup"><span data-stu-id="7cce5-128">Setting</span></span> | <span data-ttu-id="7cce5-129">name</span><span class="sxs-lookup"><span data-stu-id="7cce5-129">name</span></span> | <span data-ttu-id="7cce5-130">The Autoscale setting name.</span><span class="sxs-lookup"><span data-stu-id="7cce5-130">The Autoscale setting name.</span></span> |
| <span data-ttu-id="7cce5-131">Setting</span><span class="sxs-lookup"><span data-stu-id="7cce5-131">Setting</span></span> | <span data-ttu-id="7cce5-132">location</span><span class="sxs-lookup"><span data-stu-id="7cce5-132">location</span></span> | <span data-ttu-id="7cce5-133">The location of the Autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="7cce5-133">The location of the Autoscale setting.</span></span> <span data-ttu-id="7cce5-134">This location can be different from the location of the resource being scaled.</span><span class="sxs-lookup"><span data-stu-id="7cce5-134">This location can be different from the location of the resource being scaled.</span></span> |
| <span data-ttu-id="7cce5-135">properties</span><span class="sxs-lookup"><span data-stu-id="7cce5-135">properties</span></span> | <span data-ttu-id="7cce5-136">targetResourceUri</span><span class="sxs-lookup"><span data-stu-id="7cce5-136">targetResourceUri</span></span> | <span data-ttu-id="7cce5-137">The resource ID of the resource being scaled.</span><span class="sxs-lookup"><span data-stu-id="7cce5-137">The resource ID of the resource being scaled.</span></span> <span data-ttu-id="7cce5-138">You can only have one Autoscale setting per resource.</span><span class="sxs-lookup"><span data-stu-id="7cce5-138">You can only have one Autoscale setting per resource.</span></span> |
| <span data-ttu-id="7cce5-139">properties</span><span class="sxs-lookup"><span data-stu-id="7cce5-139">properties</span></span> | <span data-ttu-id="7cce5-140">profiles</span><span class="sxs-lookup"><span data-stu-id="7cce5-140">profiles</span></span> | <span data-ttu-id="7cce5-141">An Autoscale setting is composed of one or more profiles.</span><span class="sxs-lookup"><span data-stu-id="7cce5-141">An Autoscale setting is composed of one or more profiles.</span></span> <span data-ttu-id="7cce5-142">Each time the Autoscale engine runs, it executes one profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-142">Each time the Autoscale engine runs, it executes one profile.</span></span> |
| <span data-ttu-id="7cce5-143">profile</span><span class="sxs-lookup"><span data-stu-id="7cce5-143">profile</span></span> | <span data-ttu-id="7cce5-144">name</span><span class="sxs-lookup"><span data-stu-id="7cce5-144">name</span></span> | <span data-ttu-id="7cce5-145">The name of the profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-145">The name of the profile.</span></span> <span data-ttu-id="7cce5-146">You can choose any name that helps you identify the profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-146">You can choose any name that helps you identify the profile.</span></span> |
| <span data-ttu-id="7cce5-147">profile</span><span class="sxs-lookup"><span data-stu-id="7cce5-147">profile</span></span> | <span data-ttu-id="7cce5-148">Capacity.maximum</span><span class="sxs-lookup"><span data-stu-id="7cce5-148">Capacity.maximum</span></span> | <span data-ttu-id="7cce5-149">The maximum capacity allowed.</span><span class="sxs-lookup"><span data-stu-id="7cce5-149">The maximum capacity allowed.</span></span> <span data-ttu-id="7cce5-150">It ensures that Autoscale, when executing this profile, does not scale your resource above this number.</span><span class="sxs-lookup"><span data-stu-id="7cce5-150">It ensures that Autoscale, when executing this profile, does not scale your resource above this number.</span></span> |
| <span data-ttu-id="7cce5-151">profile</span><span class="sxs-lookup"><span data-stu-id="7cce5-151">profile</span></span> | <span data-ttu-id="7cce5-152">Capacity.minimum</span><span class="sxs-lookup"><span data-stu-id="7cce5-152">Capacity.minimum</span></span> | <span data-ttu-id="7cce5-153">The minimum capacity allowed.</span><span class="sxs-lookup"><span data-stu-id="7cce5-153">The minimum capacity allowed.</span></span> <span data-ttu-id="7cce5-154">It ensures that Autoscale, when executing this profile, does not scale your resource below this number.</span><span class="sxs-lookup"><span data-stu-id="7cce5-154">It ensures that Autoscale, when executing this profile, does not scale your resource below this number.</span></span> |
| <span data-ttu-id="7cce5-155">profile</span><span class="sxs-lookup"><span data-stu-id="7cce5-155">profile</span></span> | <span data-ttu-id="7cce5-156">Capacity.default</span><span class="sxs-lookup"><span data-stu-id="7cce5-156">Capacity.default</span></span> | <span data-ttu-id="7cce5-157">If there is a problem reading the resource metric (in this case, the CPU of “vmss1”), and the current capacity is below the default, Autoscale scales out to the default.</span><span class="sxs-lookup"><span data-stu-id="7cce5-157">If there is a problem reading the resource metric (in this case, the CPU of “vmss1”), and the current capacity is below the default, Autoscale scales out to the default.</span></span> <span data-ttu-id="7cce5-158">This is to ensure the availability of the resource.</span><span class="sxs-lookup"><span data-stu-id="7cce5-158">This is to ensure the availability of the resource.</span></span> <span data-ttu-id="7cce5-159">If the current capacity is already higher than the default capacity, Autoscale does not scale in.</span><span class="sxs-lookup"><span data-stu-id="7cce5-159">If the current capacity is already higher than the default capacity, Autoscale does not scale in.</span></span> |
| <span data-ttu-id="7cce5-160">profile</span><span class="sxs-lookup"><span data-stu-id="7cce5-160">profile</span></span> | <span data-ttu-id="7cce5-161">rules</span><span class="sxs-lookup"><span data-stu-id="7cce5-161">rules</span></span> | <span data-ttu-id="7cce5-162">Autoscale automatically scales between the maximum and minimum capacities, by using the rules in the profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-162">Autoscale automatically scales between the maximum and minimum capacities, by using the rules in the profile.</span></span> <span data-ttu-id="7cce5-163">You can have multiple rules in a profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-163">You can have multiple rules in a profile.</span></span> <span data-ttu-id="7cce5-164">Typically there are two rules: one to determine when to scale out, and the other to determine when to scale in.</span><span class="sxs-lookup"><span data-stu-id="7cce5-164">Typically there are two rules: one to determine when to scale out, and the other to determine when to scale in.</span></span> |
| <span data-ttu-id="7cce5-165">rule</span><span class="sxs-lookup"><span data-stu-id="7cce5-165">rule</span></span> | <span data-ttu-id="7cce5-166">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-166">metricTrigger</span></span> | <span data-ttu-id="7cce5-167">Defines the metric condition of the rule.</span><span class="sxs-lookup"><span data-stu-id="7cce5-167">Defines the metric condition of the rule.</span></span> |
| <span data-ttu-id="7cce5-168">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-168">metricTrigger</span></span> | <span data-ttu-id="7cce5-169">metricName</span><span class="sxs-lookup"><span data-stu-id="7cce5-169">metricName</span></span> | <span data-ttu-id="7cce5-170">The name of the metric.</span><span class="sxs-lookup"><span data-stu-id="7cce5-170">The name of the metric.</span></span> |
| <span data-ttu-id="7cce5-171">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-171">metricTrigger</span></span> |  <span data-ttu-id="7cce5-172">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="7cce5-172">metricResourceUri</span></span> | <span data-ttu-id="7cce5-173">The resource ID of the resource that emits the metric.</span><span class="sxs-lookup"><span data-stu-id="7cce5-173">The resource ID of the resource that emits the metric.</span></span> <span data-ttu-id="7cce5-174">In most cases, it is the same as the resource being scaled.</span><span class="sxs-lookup"><span data-stu-id="7cce5-174">In most cases, it is the same as the resource being scaled.</span></span> <span data-ttu-id="7cce5-175">In some cases, it can be different.</span><span class="sxs-lookup"><span data-stu-id="7cce5-175">In some cases, it can be different.</span></span> <span data-ttu-id="7cce5-176">For example, you can scale a virtual machine scale set based on the number of messages in a storage queue.</span><span class="sxs-lookup"><span data-stu-id="7cce5-176">For example, you can scale a virtual machine scale set based on the number of messages in a storage queue.</span></span> |
| <span data-ttu-id="7cce5-177">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-177">metricTrigger</span></span> | <span data-ttu-id="7cce5-178">timeGrain</span><span class="sxs-lookup"><span data-stu-id="7cce5-178">timeGrain</span></span> | <span data-ttu-id="7cce5-179">The metric sampling duration.</span><span class="sxs-lookup"><span data-stu-id="7cce5-179">The metric sampling duration.</span></span> <span data-ttu-id="7cce5-180">For example, **TimeGrain = “PT1M”** means that the metrics should be aggregated every 1 minute, by using the aggregation method specified in the statistic element.</span><span class="sxs-lookup"><span data-stu-id="7cce5-180">For example, **TimeGrain = “PT1M”** means that the metrics should be aggregated every 1 minute, by using the aggregation method specified in the statistic element.</span></span> |
| <span data-ttu-id="7cce5-181">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-181">metricTrigger</span></span> | <span data-ttu-id="7cce5-182">statistic</span><span class="sxs-lookup"><span data-stu-id="7cce5-182">statistic</span></span> | <span data-ttu-id="7cce5-183">The aggregation method within the timeGrain period.</span><span class="sxs-lookup"><span data-stu-id="7cce5-183">The aggregation method within the timeGrain period.</span></span> <span data-ttu-id="7cce5-184">For example, **statistic = “Average”** and **timeGrain = “PT1M”** means that the metrics should be aggregated every 1 minute, by taking the average.</span><span class="sxs-lookup"><span data-stu-id="7cce5-184">For example, **statistic = “Average”** and **timeGrain = “PT1M”** means that the metrics should be aggregated every 1 minute, by taking the average.</span></span> <span data-ttu-id="7cce5-185">This property dictates how the metric is sampled.</span><span class="sxs-lookup"><span data-stu-id="7cce5-185">This property dictates how the metric is sampled.</span></span> |
| <span data-ttu-id="7cce5-186">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-186">metricTrigger</span></span> | <span data-ttu-id="7cce5-187">timeWindow</span><span class="sxs-lookup"><span data-stu-id="7cce5-187">timeWindow</span></span> | <span data-ttu-id="7cce5-188">The amount of time to look back for metrics.</span><span class="sxs-lookup"><span data-stu-id="7cce5-188">The amount of time to look back for metrics.</span></span> <span data-ttu-id="7cce5-189">For example, **timeWindow = “PT10M”** means that every time Autoscale runs, it queries metrics for the past 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="7cce5-189">For example, **timeWindow = “PT10M”** means that every time Autoscale runs, it queries metrics for the past 10 minutes.</span></span> <span data-ttu-id="7cce5-190">The time window allows your metrics to be normalized, and avoids reacting to transient spikes.</span><span class="sxs-lookup"><span data-stu-id="7cce5-190">The time window allows your metrics to be normalized, and avoids reacting to transient spikes.</span></span> |
| <span data-ttu-id="7cce5-191">metricTrigger</span><span class="sxs-lookup"><span data-stu-id="7cce5-191">metricTrigger</span></span> | <span data-ttu-id="7cce5-192">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="7cce5-192">timeAggregation</span></span> | <span data-ttu-id="7cce5-193">The aggregation method used to aggregate the sampled metrics.</span><span class="sxs-lookup"><span data-stu-id="7cce5-193">The aggregation method used to aggregate the sampled metrics.</span></span> <span data-ttu-id="7cce5-194">For example, **TimeAggregation = “Average”** should aggregate the sampled metrics by taking the average.</span><span class="sxs-lookup"><span data-stu-id="7cce5-194">For example, **TimeAggregation = “Average”** should aggregate the sampled metrics by taking the average.</span></span> <span data-ttu-id="7cce5-195">In the preceding case, take the ten 1-minute samples, and average them.</span><span class="sxs-lookup"><span data-stu-id="7cce5-195">In the preceding case, take the ten 1-minute samples, and average them.</span></span> |
| <span data-ttu-id="7cce5-196">rule</span><span class="sxs-lookup"><span data-stu-id="7cce5-196">rule</span></span> | <span data-ttu-id="7cce5-197">scaleAction</span><span class="sxs-lookup"><span data-stu-id="7cce5-197">scaleAction</span></span> | <span data-ttu-id="7cce5-198">The action to take when the metricTrigger of the rule is triggered.</span><span class="sxs-lookup"><span data-stu-id="7cce5-198">The action to take when the metricTrigger of the rule is triggered.</span></span> |
| <span data-ttu-id="7cce5-199">scaleAction</span><span class="sxs-lookup"><span data-stu-id="7cce5-199">scaleAction</span></span> | <span data-ttu-id="7cce5-200">direction</span><span class="sxs-lookup"><span data-stu-id="7cce5-200">direction</span></span> | <span data-ttu-id="7cce5-201">"Increase" to scale out, or "Decrease" to scale in.</span><span class="sxs-lookup"><span data-stu-id="7cce5-201">"Increase" to scale out, or "Decrease" to scale in.</span></span>|
| <span data-ttu-id="7cce5-202">scaleAction</span><span class="sxs-lookup"><span data-stu-id="7cce5-202">scaleAction</span></span> | <span data-ttu-id="7cce5-203">value</span><span class="sxs-lookup"><span data-stu-id="7cce5-203">value</span></span> | <span data-ttu-id="7cce5-204">How much to increase or decrease the capacity of the resource.</span><span class="sxs-lookup"><span data-stu-id="7cce5-204">How much to increase or decrease the capacity of the resource.</span></span> |
| <span data-ttu-id="7cce5-205">scaleAction</span><span class="sxs-lookup"><span data-stu-id="7cce5-205">scaleAction</span></span> | <span data-ttu-id="7cce5-206">cooldown</span><span class="sxs-lookup"><span data-stu-id="7cce5-206">cooldown</span></span> | <span data-ttu-id="7cce5-207">The amount of time to wait after a scale operation before scaling again.</span><span class="sxs-lookup"><span data-stu-id="7cce5-207">The amount of time to wait after a scale operation before scaling again.</span></span> <span data-ttu-id="7cce5-208">For example, if **cooldown = “PT10M”**, Autoscale does not attempt to scale again for another 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="7cce5-208">For example, if **cooldown = “PT10M”**, Autoscale does not attempt to scale again for another 10 minutes.</span></span> <span data-ttu-id="7cce5-209">The cooldown is to allow the metrics to stabilize after the addition or removal of instances.</span><span class="sxs-lookup"><span data-stu-id="7cce5-209">The cooldown is to allow the metrics to stabilize after the addition or removal of instances.</span></span> |

## <a name="autoscale-profiles"></a><span data-ttu-id="7cce5-210">Autoscale profiles</span><span class="sxs-lookup"><span data-stu-id="7cce5-210">Autoscale profiles</span></span>

<span data-ttu-id="7cce5-211">There are three types of Autoscale profiles:</span><span class="sxs-lookup"><span data-stu-id="7cce5-211">There are three types of Autoscale profiles:</span></span>

- <span data-ttu-id="7cce5-212">**Regular profile:** The most common profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-212">**Regular profile:** The most common profile.</span></span> <span data-ttu-id="7cce5-213">If you don’t need to scale your resource based on the day of the week, or on a particular day, you can use a regular profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-213">If you don’t need to scale your resource based on the day of the week, or on a particular day, you can use a regular profile.</span></span> <span data-ttu-id="7cce5-214">This profile can then be configured with metric rules that dictate when to scale out and when to scale in.</span><span class="sxs-lookup"><span data-stu-id="7cce5-214">This profile can then be configured with metric rules that dictate when to scale out and when to scale in.</span></span> <span data-ttu-id="7cce5-215">You should only have one regular profile defined.</span><span class="sxs-lookup"><span data-stu-id="7cce5-215">You should only have one regular profile defined.</span></span>

    <span data-ttu-id="7cce5-216">The example profile used earlier in this article is an example of a regular profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-216">The example profile used earlier in this article is an example of a regular profile.</span></span> <span data-ttu-id="7cce5-217">Note that it is also possible to set a profile to scale to a static instance count for your resource.</span><span class="sxs-lookup"><span data-stu-id="7cce5-217">Note that it is also possible to set a profile to scale to a static instance count for your resource.</span></span>

- <span data-ttu-id="7cce5-218">**Fixed date profile:** This profile is for special cases.</span><span class="sxs-lookup"><span data-stu-id="7cce5-218">**Fixed date profile:** This profile is for special cases.</span></span> <span data-ttu-id="7cce5-219">For example, let’s say you have an important event coming up on December 26, 2017 (PST).</span><span class="sxs-lookup"><span data-stu-id="7cce5-219">For example, let’s say you have an important event coming up on December 26, 2017 (PST).</span></span> <span data-ttu-id="7cce5-220">You want the minimum and maximum capacities of your resource to be different on that day, but still scale on the same metrics.</span><span class="sxs-lookup"><span data-stu-id="7cce5-220">You want the minimum and maximum capacities of your resource to be different on that day, but still scale on the same metrics.</span></span> <span data-ttu-id="7cce5-221">In this case, you should add a fixed date profile to your setting’s list of profiles.</span><span class="sxs-lookup"><span data-stu-id="7cce5-221">In this case, you should add a fixed date profile to your setting’s list of profiles.</span></span> <span data-ttu-id="7cce5-222">The profile is configured to run only on the event’s day.</span><span class="sxs-lookup"><span data-stu-id="7cce5-222">The profile is configured to run only on the event’s day.</span></span> <span data-ttu-id="7cce5-223">For any other day, Autoscale uses the regular profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-223">For any other day, Autoscale uses the regular profile.</span></span>

    ``` JSON
    "profiles": [{
    "name": " regularProfile",
    "capacity": {
    ...
    },
    "rules": [{
    ...
    },
    {
    ...
    }]
    },
    {
    "name": "eventProfile",
    "capacity": {
    ...
    },
    "rules": [{
    ...
    }, {
    ...
    }],
    "fixedDate": {
        "timeZone": "Pacific Standard Time",
               "start": "2017-12-26T00:00:00",
               "end": "2017-12-26T23:59:00"
    }}
    ]
    ```
    
- <span data-ttu-id="7cce5-224">**Recurrence profile:** This type of profile enables you to ensure that this profile is always used on a particular day of the week.</span><span class="sxs-lookup"><span data-stu-id="7cce5-224">**Recurrence profile:** This type of profile enables you to ensure that this profile is always used on a particular day of the week.</span></span> <span data-ttu-id="7cce5-225">Recurrence profiles only have a start time.</span><span class="sxs-lookup"><span data-stu-id="7cce5-225">Recurrence profiles only have a start time.</span></span> <span data-ttu-id="7cce5-226">They run until the next recurrence profile or fixed date profile is set to start.</span><span class="sxs-lookup"><span data-stu-id="7cce5-226">They run until the next recurrence profile or fixed date profile is set to start.</span></span> <span data-ttu-id="7cce5-227">An Autoscale setting with only one recurrence profile runs that profile, even if there is a regular profile defined in the same setting.</span><span class="sxs-lookup"><span data-stu-id="7cce5-227">An Autoscale setting with only one recurrence profile runs that profile, even if there is a regular profile defined in the same setting.</span></span> <span data-ttu-id="7cce5-228">The following two examples illustrate how this profile is used:</span><span class="sxs-lookup"><span data-stu-id="7cce5-228">The following two examples illustrate how this profile is used:</span></span>

    <span data-ttu-id="7cce5-229">**Example 1: Weekdays vs. weekends**</span><span class="sxs-lookup"><span data-stu-id="7cce5-229">**Example 1: Weekdays vs. weekends**</span></span>
    
    <span data-ttu-id="7cce5-230">Let’s say that on weekends, you want your maximum capacity to be 4.</span><span class="sxs-lookup"><span data-stu-id="7cce5-230">Let’s say that on weekends, you want your maximum capacity to be 4.</span></span> <span data-ttu-id="7cce5-231">On weekdays, because you expect more load, you want your maximum capacity to be 10.</span><span class="sxs-lookup"><span data-stu-id="7cce5-231">On weekdays, because you expect more load, you want your maximum capacity to be 10.</span></span> <span data-ttu-id="7cce5-232">In this case, your setting would contain two recurrence profiles, one to run on weekends and the other on weekdays.</span><span class="sxs-lookup"><span data-stu-id="7cce5-232">In this case, your setting would contain two recurrence profiles, one to run on weekends and the other on weekdays.</span></span>
    <span data-ttu-id="7cce5-233">The setting looks like this:</span><span class="sxs-lookup"><span data-stu-id="7cce5-233">The setting looks like this:</span></span>

    ``` JSON
    "profiles": [
    {
    "name": "weekdayProfile",
    "capacity": {
        ...
    },
    "rules": [{
        ...
    }],
    "recurrence": {
        "frequency": "Week",
        "schedule": {
            "timeZone": "Pacific Standard Time",
            "days": [
                "Monday"
            ],
            "hours": [
                0
            ],
            "minutes": [
                0
            ]
        }
    }}
    },
    {
    "name": "weekendProfile",
    "capacity": {
        ...
    },
    "rules": [{
        ...
    }]
    "recurrence": {
        "frequency": "Week",
        "schedule": {
            "timeZone": "Pacific Standard Time",
            "days": [
                "Saturday"
            ],
            "hours": [
                0
            ],
            "minutes": [
                0
            ]
        }
    }
    }]
    ```

    <span data-ttu-id="7cce5-234">The preceding setting shows that each recurrence profile has a schedule.</span><span class="sxs-lookup"><span data-stu-id="7cce5-234">The preceding setting shows that each recurrence profile has a schedule.</span></span> <span data-ttu-id="7cce5-235">This schedule determines when the profile starts running.</span><span class="sxs-lookup"><span data-stu-id="7cce5-235">This schedule determines when the profile starts running.</span></span> <span data-ttu-id="7cce5-236">The profile stops when it’s time to run another profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-236">The profile stops when it’s time to run another profile.</span></span>

    <span data-ttu-id="7cce5-237">For example, in the preceding setting, “weekdayProfile” is set to start on Monday at 12:00 AM.</span><span class="sxs-lookup"><span data-stu-id="7cce5-237">For example, in the preceding setting, “weekdayProfile” is set to start on Monday at 12:00 AM.</span></span> <span data-ttu-id="7cce5-238">That means this profile starts running on Monday at 12:00 AM.</span><span class="sxs-lookup"><span data-stu-id="7cce5-238">That means this profile starts running on Monday at 12:00 AM.</span></span> <span data-ttu-id="7cce5-239">It continues until Saturday at 12:00 AM, when “weekendProfile”  is scheduled to start running.</span><span class="sxs-lookup"><span data-stu-id="7cce5-239">It continues until Saturday at 12:00 AM, when “weekendProfile”  is scheduled to start running.</span></span>

    <span data-ttu-id="7cce5-240">**Example 2: Business hours**</span><span class="sxs-lookup"><span data-stu-id="7cce5-240">**Example 2: Business hours**</span></span>
    
    <span data-ttu-id="7cce5-241">Let's say you want to have one metric threshold during business hours (9:00 AM to 5:00 PM), and a different one for all other times.</span><span class="sxs-lookup"><span data-stu-id="7cce5-241">Let's say you want to have one metric threshold during business hours (9:00 AM to 5:00 PM), and a different one for all other times.</span></span> <span data-ttu-id="7cce5-242">The setting would look like this:</span><span class="sxs-lookup"><span data-stu-id="7cce5-242">The setting would look like this:</span></span>
    
    ``` JSON
    "profiles": [
    {
    "name": "businessHoursProfile",
    "capacity": {
        ...
    },
    "rules": [{
        ...
    }],
    "recurrence": {
        "frequency": "Week",
        "schedule": {
            "timeZone": "Pacific Standard Time",
            "days": [
                "Monday", “Tuesday”, “Wednesday”, “Thursday”, “Friday”
            ],
            "hours": [
                9
            ],
            "minutes": [
                0
            ]
        }
    }
    },
    {
    "name": "nonBusinessHoursProfile",
    "capacity": {
        ...
    },
    "rules": [{
        ...
    }]
    "recurrence": {
        "frequency": "Week",
        "schedule": {
            "timeZone": "Pacific Standard Time",
            "days": [
                "Monday", “Tuesday”, “Wednesday”, “Thursday”, “Friday”
            ],
            "hours": [
                17
            ],
            "minutes": [
                0
            ]
        }
    }
    }]
    ```
    
    <span data-ttu-id="7cce5-243">The preceding setting shows that “businessHoursProfile” begins running on Monday at 9:00 AM, and continues to 5:00 PM.</span><span class="sxs-lookup"><span data-stu-id="7cce5-243">The preceding setting shows that “businessHoursProfile” begins running on Monday at 9:00 AM, and continues to 5:00 PM.</span></span> <span data-ttu-id="7cce5-244">That’s when “nonBusinessHoursProfile” starts running.</span><span class="sxs-lookup"><span data-stu-id="7cce5-244">That’s when “nonBusinessHoursProfile” starts running.</span></span> <span data-ttu-id="7cce5-245">The “nonBusinessHoursProfile” runs until 9:00 AM Tuesday, and then the “businessHoursProfile” takes over again.</span><span class="sxs-lookup"><span data-stu-id="7cce5-245">The “nonBusinessHoursProfile” runs until 9:00 AM Tuesday, and then the “businessHoursProfile” takes over again.</span></span> <span data-ttu-id="7cce5-246">This repeats until Friday at 5:00 PM.</span><span class="sxs-lookup"><span data-stu-id="7cce5-246">This repeats until Friday at 5:00 PM.</span></span> <span data-ttu-id="7cce5-247">At that point, “nonBusinessHoursProfile” runs all the way to Monday at 9:00 AM.</span><span class="sxs-lookup"><span data-stu-id="7cce5-247">At that point, “nonBusinessHoursProfile” runs all the way to Monday at 9:00 AM.</span></span>
    
> [!Note]
> <span data-ttu-id="7cce5-248">The Autoscale user interface in the Azure portal enforces end times for recurrence profiles, and begins running the Autoscale setting's default profile in between recurrence profiles.</span><span class="sxs-lookup"><span data-stu-id="7cce5-248">The Autoscale user interface in the Azure portal enforces end times for recurrence profiles, and begins running the Autoscale setting's default profile in between recurrence profiles.</span></span>
    
## <a name="autoscale-evaluation"></a><span data-ttu-id="7cce5-249">Autoscale evaluation</span><span class="sxs-lookup"><span data-stu-id="7cce5-249">Autoscale evaluation</span></span>
<span data-ttu-id="7cce5-250">Given that Autoscale settings can have multiple profiles, and each profile can have multiple metric rules, it is important to understand how an Autoscale setting is evaluated.</span><span class="sxs-lookup"><span data-stu-id="7cce5-250">Given that Autoscale settings can have multiple profiles, and each profile can have multiple metric rules, it is important to understand how an Autoscale setting is evaluated.</span></span> <span data-ttu-id="7cce5-251">Each time the Autoscale job runs, it begins by choosing the profile that is applicable.</span><span class="sxs-lookup"><span data-stu-id="7cce5-251">Each time the Autoscale job runs, it begins by choosing the profile that is applicable.</span></span> <span data-ttu-id="7cce5-252">Then Autoscale evaluates the minimum and maximum values, and any metric rules in the profile, and decides if a scale action is necessary.</span><span class="sxs-lookup"><span data-stu-id="7cce5-252">Then Autoscale evaluates the minimum and maximum values, and any metric rules in the profile, and decides if a scale action is necessary.</span></span>

### <a name="which-profile-will-autoscale-pick"></a><span data-ttu-id="7cce5-253">Which profile will Autoscale pick?</span><span class="sxs-lookup"><span data-stu-id="7cce5-253">Which profile will Autoscale pick?</span></span>

<span data-ttu-id="7cce5-254">Autoscale uses the following sequence to pick the profile:</span><span class="sxs-lookup"><span data-stu-id="7cce5-254">Autoscale uses the following sequence to pick the profile:</span></span>
1. <span data-ttu-id="7cce5-255">It first looks for any fixed date profile that is configured to run now.</span><span class="sxs-lookup"><span data-stu-id="7cce5-255">It first looks for any fixed date profile that is configured to run now.</span></span> <span data-ttu-id="7cce5-256">If there is, Autoscale runs it.</span><span class="sxs-lookup"><span data-stu-id="7cce5-256">If there is, Autoscale runs it.</span></span> <span data-ttu-id="7cce5-257">If there are multiple fixed date profiles that are supposed to run, Autoscale selects the first one.</span><span class="sxs-lookup"><span data-stu-id="7cce5-257">If there are multiple fixed date profiles that are supposed to run, Autoscale selects the first one.</span></span>
2. <span data-ttu-id="7cce5-258">If there are no fixed date profiles, Autoscale looks at recurrence profiles.</span><span class="sxs-lookup"><span data-stu-id="7cce5-258">If there are no fixed date profiles, Autoscale looks at recurrence profiles.</span></span> <span data-ttu-id="7cce5-259">If a recurrence profile is found, it runs it.</span><span class="sxs-lookup"><span data-stu-id="7cce5-259">If a recurrence profile is found, it runs it.</span></span>
3. <span data-ttu-id="7cce5-260">If there are no fixed date or recurrence profiles, Autoscale runs the regular profile.</span><span class="sxs-lookup"><span data-stu-id="7cce5-260">If there are no fixed date or recurrence profiles, Autoscale runs the regular profile.</span></span>

### <a name="how-does-autoscale-evaluate-multiple-rules"></a><span data-ttu-id="7cce5-261">How does Autoscale evaluate multiple rules?</span><span class="sxs-lookup"><span data-stu-id="7cce5-261">How does Autoscale evaluate multiple rules?</span></span>

<span data-ttu-id="7cce5-262">After Autoscale determines which profile to run, it evaluates all the scale-out rules in the profile (these are rules with **direction = “Increase”**).</span><span class="sxs-lookup"><span data-stu-id="7cce5-262">After Autoscale determines which profile to run, it evaluates all the scale-out rules in the profile (these are rules with **direction = “Increase”**).</span></span>

<span data-ttu-id="7cce5-263">If one or more scale-out rules are triggered, Autoscale calculates the new capacity determined by the **scaleAction** of each of those rules.</span><span class="sxs-lookup"><span data-stu-id="7cce5-263">If one or more scale-out rules are triggered, Autoscale calculates the new capacity determined by the **scaleAction** of each of those rules.</span></span> <span data-ttu-id="7cce5-264">Then it scales out to the maximum of those capacities, to ensure service availability.</span><span class="sxs-lookup"><span data-stu-id="7cce5-264">Then it scales out to the maximum of those capacities, to ensure service availability.</span></span>

<span data-ttu-id="7cce5-265">For example, let's say there is a virtual machine scale set with a current capacity of 10.</span><span class="sxs-lookup"><span data-stu-id="7cce5-265">For example, let's say there is a virtual machine scale set with a current capacity of 10.</span></span> <span data-ttu-id="7cce5-266">There are two scale-out rules: one that increases capacity by 10 percent, and one that increases capacity by 3 counts.</span><span class="sxs-lookup"><span data-stu-id="7cce5-266">There are two scale-out rules: one that increases capacity by 10 percent, and one that increases capacity by 3 counts.</span></span> <span data-ttu-id="7cce5-267">The first rule would result in a new capacity of 11, and the second rule would result in a capacity of 13.</span><span class="sxs-lookup"><span data-stu-id="7cce5-267">The first rule would result in a new capacity of 11, and the second rule would result in a capacity of 13.</span></span> <span data-ttu-id="7cce5-268">To ensure service availability, Autoscale chooses the action that results in the maximum capacity, so the second rule is chosen.</span><span class="sxs-lookup"><span data-stu-id="7cce5-268">To ensure service availability, Autoscale chooses the action that results in the maximum capacity, so the second rule is chosen.</span></span>

<span data-ttu-id="7cce5-269">If no scale-out rules are triggered, Autoscale evaluates all the scale-in rules (rules with **direction = “Decrease”**).</span><span class="sxs-lookup"><span data-stu-id="7cce5-269">If no scale-out rules are triggered, Autoscale evaluates all the scale-in rules (rules with **direction = “Decrease”**).</span></span> <span data-ttu-id="7cce5-270">Autoscale only takes a scale-in action if all of the scale-in rules are triggered.</span><span class="sxs-lookup"><span data-stu-id="7cce5-270">Autoscale only takes a scale-in action if all of the scale-in rules are triggered.</span></span>

<span data-ttu-id="7cce5-271">Autoscale calculates the new capacity determined by the **scaleAction** of each of those rules.</span><span class="sxs-lookup"><span data-stu-id="7cce5-271">Autoscale calculates the new capacity determined by the **scaleAction** of each of those rules.</span></span> <span data-ttu-id="7cce5-272">Then it chooses the scale action that results in the maximum of those capacities to ensure service availability.</span><span class="sxs-lookup"><span data-stu-id="7cce5-272">Then it chooses the scale action that results in the maximum of those capacities to ensure service availability.</span></span>

<span data-ttu-id="7cce5-273">For example, let's say there is a virtual machine scale set with a current capacity of 10.</span><span class="sxs-lookup"><span data-stu-id="7cce5-273">For example, let's say there is a virtual machine scale set with a current capacity of 10.</span></span> <span data-ttu-id="7cce5-274">There are two scale-in rules: one that decreases capacity by 50 percent, and one that decreases capacity by 3 counts.</span><span class="sxs-lookup"><span data-stu-id="7cce5-274">There are two scale-in rules: one that decreases capacity by 50 percent, and one that decreases capacity by 3 counts.</span></span> <span data-ttu-id="7cce5-275">The first rule would result in a new capacity of 5, and the second rule would result in a capacity of 7.</span><span class="sxs-lookup"><span data-stu-id="7cce5-275">The first rule would result in a new capacity of 5, and the second rule would result in a capacity of 7.</span></span> <span data-ttu-id="7cce5-276">To ensure service availability, Autoscale chooses the action that results in the maximum capacity, so the second rule is chosen.</span><span class="sxs-lookup"><span data-stu-id="7cce5-276">To ensure service availability, Autoscale chooses the action that results in the maximum capacity, so the second rule is chosen.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cce5-277">Next steps</span><span class="sxs-lookup"><span data-stu-id="7cce5-277">Next steps</span></span>
<span data-ttu-id="7cce5-278">Learn more about Autoscale by referring to the following:</span><span class="sxs-lookup"><span data-stu-id="7cce5-278">Learn more about Autoscale by referring to the following:</span></span>

* [<span data-ttu-id="7cce5-279">Overview of autoscale</span><span class="sxs-lookup"><span data-stu-id="7cce5-279">Overview of autoscale</span></span>](monitoring-overview-autoscale.md)
* [<span data-ttu-id="7cce5-280">Azure Monitor autoscale common metrics</span><span class="sxs-lookup"><span data-stu-id="7cce5-280">Azure Monitor autoscale common metrics</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="7cce5-281">Best practices for Azure Monitor autoscale</span><span class="sxs-lookup"><span data-stu-id="7cce5-281">Best practices for Azure Monitor autoscale</span></span>](insights-autoscale-best-practices.md)
* [<span data-ttu-id="7cce5-282">Use autoscale actions to send email and webhook alert notifications</span><span class="sxs-lookup"><span data-stu-id="7cce5-282">Use autoscale actions to send email and webhook alert notifications</span></span>](insights-autoscale-to-webhook-email.md)
* [<span data-ttu-id="7cce5-283">Autoscale REST API</span><span class="sxs-lookup"><span data-stu-id="7cce5-283">Autoscale REST API</span></span>](https://msdn.microsoft.com/library/dn931953.aspx)
