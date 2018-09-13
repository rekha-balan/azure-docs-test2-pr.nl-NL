---
title: Best practices for autoscaling | Microsoft Docs
description: Learn principles to effectively autoscale Virtual Machines, Virtual Machine Scale Sets, and Cloud Services.
author: kamathashwin
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2016
ms.author: ashwink
ms.openlocfilehash: 0f0f0c2d02be573b1b2c94394d390e3ae7d48510
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540900"
---
# <a name="best-practices-autoscaling-virtual"></a>Best practices Autoscaling Virtual
This article teaches best practices to autoscale in Azure. It relates to Virtual Machines, Virtual Machine Scale Sets and Cloud Services.  Other Azure services used different scaling methods.

## <a name="autoscale-concepts"></a>Autoscale concepts
* A resource can have only *one* autoscale setting
* An autoscale setting can have one or more profiles and each profile can have one or more autoscale rules.
* An autoscale setting scales instances horizontally, which is *out* by increasing the instances and *in* by decreasing the number of instances.
  An autoscale setting has a maximum, minimum, and default value of instances.
* An autoscale job always reads the associated metric to scale by, checking if it has crossed the configured threshold for scale-out or scale-in. You can view a list of metrics that autoscale can scale by at [Azure Monitor autoscaling common metrics](insights-autoscale-common-metrics.md).
* All thresholds are calculated at an instance level. For example, "scale out by 1 instance when average CPU > 80% when instance count is 2", means scale-out when the average CPU across all instances is greater than 80%.
* You always receive failure notifications via email. Specifically, the owner, contributor, and readers of the target resource receive email. You also always receive a *recovery* email when autoscale recovers from a failure and starts functioning normally.
* You can opt-in to receive a successful scale action notification via email and webhooks.

## <a name="autoscale-best-practices"></a>Autoscale best practices
Use the following best practices as you use autoscale.

### <a name="ensure-the-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Ensure the maximum and minimum values are different and have an adequate margin between them
If you have a setting that has minimum=2, maximum=2 and the current instance count is 2, no scale action can occur. Keep an adequate margin between the maximum and minimum instance counts, which are inclusive. Autoscale always scales between these limits.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>Manual scaling is reset by autoscale min and max
If you manually update the instance count to a value above or below the maximum, the autoscale engine automatically scales back to the minimum (if below) or the maximum (if above). For example, you set the range between 3 and 6. If you have one running instance, the autoscale engine scales to 3 instances on its next run. Likewise, it would scale-in 8 instances back to 6 on its next run.  Manual scaling is very temporary unless you reset the autoscale rules as well.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Always use a scale-out and scale-in rule combination that performs an increase and decrease
If you use only one part of the combination, autoscale scale-in that single out, or in, until the maximum, or minimum, is reached.

### <a name="do-not-switch-between-the-azure-portal-and-the-azure-classic-portal-when-managing-autoscale"></a>Do not switch between the Azure portal and the Azure classic portal when managing Autoscale
For Cloud Services and App Services (Web Apps), use the Azure portal (portal.azure.com) to create and manage autoscale settings. For Virtual Machine Scale Sets use PowerShell, CLI or REST API to create and manage autoscale setting. Do not switch between the Azure classic portal (manage.windowsazure.com) and the Azure portal (portal.azure.com) when managing autoscale configurations. The Azure classic portal and its underlying backend has limitations. Move to the Azure portal to manage autoscale using a graphical user interface. The options are to use the autoscale PowerShell, CLI or REST API (via Azure Resource Explorer).

### <a name="choose-the-appropriate-statistic-for-your-diagnostics-metric"></a>Choose the appropriate statistic for your diagnostics metric
For diagnostics metrics, you can choose among *Average*, *Minimum*, *Maximum* and *Total* as a metric to scale by. The most common statistic is *Average*.

### <a name="choose-the-thresholds-carefully-for-all-metric-types"></a>Choose the thresholds carefully for all metric types
We recommend carefully choosing different thresholds for scale-out and scale-in based on practical situations.

We *do not recommend* autoscale settings like the examples below with the same or very similar threshold values for out and in conditions:

* Increase instances by 1 count when Thread Count <= 600
* Decrease instances by 1 count when Thread Count >= 600

Let's look at an example of what can lead to a behavior that may seem confusing. Consider the following sequence.

1. Assume there are 2 instances to begin with and then the average number of threads per instance grows to 625.
2. Autoscale scales out adding a 3rd instance.
3. Next, assume that the average thread count across instance falls to 575.
4. Before scaling down, autoscale tries to estimate what the final state will be if it scaled in. For example, 575 x  3 (current instance count) = 1,725 / 2 (final number of instances when scaled down) = 862.5 threads. This means autoscale would have to immediately scale-out again even after it scaled in, if the average thread count remains the same or even falls only a small amount. However, if it scaled up again, the whole process would repeat, leading to an infinite loop.
5. To avoid this situation (termed "flapping"), autoscale does not scale down at all. Instead, it skips and reevaluates the condition again the next time the service's job executes. This could confuse many people because autoscale wouldn't appear to work when the average thread count was 575.

Estimation during a scale-in is intended to avoid "flapping" situations, where scale-in and scale-out actions continually go back and forth. Keep this behavior in mind when you choose the same thresholds for scale-out and in.

We recommend choosing an adequate margin between the scale-out and in thresholds. As an example, consider the following better rule combination.

* Increase instances by 1 count when CPU%  >= 80
* Decrease instances by 1 count when CPU% <= 60

In this case  

1. Assume there are 2 instances to start with.
2. If the average CPU% across instances goes to 80, autoscale scales out adding a third instance.
3. Now assume that over time the CPU% falls to 60.
4. Autoscale's scale-in rule estimates the final state if it were to scale-in. For example, 60 x 3 (current instance count) = 180 / 2 (final number of instances when scaled down) = 90. So autoscale does not scale-in because it would have to scale-out again immediately. Instead, it skips scaling down.
5. The next time autoscale checks, the CPU continues to fall to 50. It estimates again -  50 x 3 instance = 150 / 2 instances = 75, which is below the scale-out threshold of 80, so it scales in successfully to 2 instances.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Considerations for scaling threshold values for special metrics
 For special metrics such as Storage or Service Bus Queue length metric, the threshold is the average number of messages available per current number of instances. Carefully choose the choose the threshold value for this metric.

Let's illustrate it with an example to ensure you understand the behavior better.

* Increase instances by 1 count when Storage Queue message count >= 50
* Decrease instances by 1 count when Storage Queue message count <= 10

Consider the following sequence:

1. There are 2 storage queue instances.
2. Messages keep coming and when you review the storage queue, the total count reads 50. You might assume that autoscale should start a scale-out action. However, note that it is still 50/2 = 25 messages per instance. So, scale-out does not occur. For the first scale-out to happen, the total message count in the storage queue should be 100.
3. Next, assume that the total message count reaches 100.
4. A 3rd storage queue instance is added due to a scale-out action.  The next scale-out action will not happen until the total message count in the queue reaches 150 because 150/3 = 50.
5. Now the number of messages in the queue gets smaller. With 3 instances, the first scale-in action happens when the total messages in all queues add up to 30 because 30/3 = 10 messages per instance, which is the scale-in threshold.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Considerations for scaling when multiple profiles are configured in an autoscale setting
In an autoscale setting, you can choose a default profile, which is always applied without any dependency on schedule or time, or you can choose a recurring profile or a profile for a fixed period with a date and time range.

When autoscale service processes them, it always checks in the following order:

1. Fixed Date profile
2. Recurring profile
3. Default ("Always") profile

If a profile condition is met, autoscale does not check the next profile condition below it. Autoscale only processes one profile at a time. This means if you want to also include a processing condition from a lower-tier profile, you must include those rules as well in the current profile.

Let's review this using an example:

The image below shows an autoscale setting with a default profile of minimum instances = 2 and maximum instances = 10. In this example, rules are configured to scale-out when the message count in the queue is greater than 10 and scale-in when the message count in the queue is less than 3. So now the resource can scale between 2 and 10 instances.

In addition, there is a recurring profile set for Monday. It is set for minimum instances = 2 and maximum instances = 12. This means on Monday, the first time autoscale checks for this condition, if the instance count is 2, it scales to the new minimum of 3. As long as autoscale continues to find this profile condition matched (Monday), it only processes the CPU-based scale-out/in rules configured for this profile. At this time, it does not check for the queue length. However, if you also want the queue length condition to be checked, you should include those rules from the default profile as well in your Monday profile.

Similarly, when autoscale switches back to the default profile, it first checks if the minimum and maximum conditions are met. If the number of instances at the time is 12, it scales in to 10, the maximum allowed for the default profile.

![autoscale settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-autoscale-best-practices/insights-autoscale-best-practices.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Considerations for scaling when multiple rules are configured in a profile
There are cases where you may have to set multiple rules in a profile. The following set of autoscale rules are used by services use when multiple rules are set.

On *scale out*, autoscale runs if any rule is met.
On *scale-in*, autoscale require all rules to be met.

To illustrate, assume that you have the following 4 autoscale rules:

* If CPU < 30 %, scale-in by 1
* If Memory < 50%, scale-in by 1
* If CPU > 75%, scale-out by 1
* If Memory > 75%, scale-out by 1

Then the follow occurs:

* If CPU is 76% and Memory is 50%, we scale-out.
* If CPU is 50% and Memory is 76% we scale-out.

On the other hand, if CPU is 25% and memory is 51% autoscale does **not** scale-in. In order to scale-in, CPU must be 29% and Memory 49%.

### <a name="always-select-a-safe-default-instance-count"></a>Always select a safe default instance count
The default instance count is important autoscale scales your service to that count when metrics are not available. Therefore, select a default instance count that's safe for your workloads.

### <a name="configure-autoscale-notifications"></a>Configure autoscale notifications
Autoscale notifies the administrators and contributors of the resource by email if any of the following conditions occur:

* autoscale service fails to take an action.
* Metrics are not available for autoscale service to make a scale decision.
* Metrics are available (recovery) again to make a scale decision.
  In addition to the conditions above, you can configure email or webhook notifications to get notified for successful scale actions.

